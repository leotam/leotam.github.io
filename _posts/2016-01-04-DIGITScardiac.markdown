---
layout: post
title:  "Cardiac Regression with DiGITS"
date:   2016-01-04 15:00:00
categories: general
---

This year NVIDIA is co-sponsoring the National Data Science Bowl [competition][kaggleLink] on cardiac volume prediction.  Regression, where a model generates a real number (as opposed to the discrete case of classification) is the relevant challenge here.  In this presentation, [DiGITS][digits] sitting on top of Caffe is used for cardiac MR CINE (volumetric video acquisition) end diastolic and systolic LV volume prediction.  The model currently achieves 0.049108 (lower is better) on the metric (Continuous Ranked Probability Score (CRPS) ) with just a basic Lenet.

DiGITS is a graphical interface with handy real-time visualization of model training.  It is accessible to the starting DL researcher and useful for the more advanced user.  For the competition here, the model finetuning and easily accessible hyper-parameter management will prove useful in phase II, where the validation labels are released.  The software requirements are DiGITs 3 which now has [deb packages][deb] installation for Ubuntu 14.04.  Other required software includes Python 2.X and the associated packages used, eg. pydicom, numpy, scipy.  The dataset is obtained through the [Kaggle website][kagCardiac].

We run a number of preprocessing scripts to extract the data from DICOM format using [pydicom][pydicom].  Before running the scripts, copy a skeleton directory structure to destination folder via a terminal, eg. 

sudo find -type d -links 2 -exec mkdir -p "/raid/leo/cardiac/trainDigits/{}" \;

Run this in the folder that you've put all your training images, eg. /raid/leo/cardiac/train.  Now run the preprocessing [script][preproc] which will extract frames of 27 cardiac MR images, nearly representing a cardiac cycle, and reshape them into a single image composed of 3x3 tiles x3 channels (false RGB).  Make sure to change data paths on lines 165-172 to match your file system.

![IM5306falseColorHeart]({{ site.url }}/assets/IM5306falseColorHeartV2.JPG)

*27 sequential cardiac images are tiled and stacked to create a false color image.  What do the colored regions represent and what in what domains does a convolution act on this image?*

Interestingly, convolutions now act spatially and temporally since the image is composed of a time series of images.  When the preprocessing is done, fire up DIGITs 3.0.

Non-classification datasets may be created in DiGITS through the "other" type of datasets. For these datasets, DiGITS expects the user to provide a set of LMDB databases. Note that since labels may be vectors (or matrices), it is not possible to use a single LMDB database to hold the image and its label. Therefore, DiGITS expects one LMDB database for the images and a separate LMDB database for the labels.
 
Writing the LMDB in Python:

{% highlight python %}
def _write_to_lmdb(db, key, value):
   """
   Write (key,value) to db
   """
   success = False
   while not success:
       txn = db.begin(write=True)
       try:
           txn.put(key, value)
           txn.commit()
           success = True
       except lmdb.MapFullError:
           txn.abort()

           # double the map_size
           curr_limit = db.info()['map_size']
           new_limit = curr_limit*2
           print '>>> Doubling LMDB map size to %sMB ...' % (new_limit>>20,)
           db.set_mapsize(new_limit) # double it
{% endhighlight %}

In the generic dataset creation form, you need to provide the paths to:

  1. the train image database (eg. /raid/leo/cardiac/trainDigits/train_images)

  2. the train label database (eg. /raid/leo/cardiac/trainDigits/train_labels)

  3. the train mean image train_mean.binaryproto file (eg. /raid/leo/cardiac/trainDigits/train_mean.binaryproto)

Once the dataset has been created, create an 'other' model to generate a regression model. Paste in the prototxt file for [a basic Lenet][Lenet].  For solver options, set the base learning rate to 1e-8, click advanced learning rate options and select 65% for the set size %. 

![digitsModelHyperparams]({{ site.url }}/assets/digitsModelHyperparamsV2.PNG)

*Enter in the model hyperparameters via DiGITS as depicted*

Once your model is trained, push validation images file list through the model using the 'Test Many' to create predictions for end diastolic and systolic LV volume prediction. Here is a [sample list][valList].  Several of these scripts were based off of Bing Xu's [Mxnet tutorial][mxnet] and other code from the NVIDIA DiGITS repository.  If submitting for evaluation on the leaderboard, a Python [script formats][submit] the predictions in terms of a cumulative probability distribution function. 

There are many improvements that can be made to this initial approach, aside from the possibilites of a new direction that DiGITS may bring to your workflow.  Improvements include extending the regression to predict 600 values of the probability distribution, improved networks such as AlexNet or GoogLeNet (example protobuf files in DiGITS), data augmentation of the network (maybe rearranging time sequence), different loss functions, hyperparameter adjustments, etc.

Happy competing!

[kaggleLink]: https://www.kaggle.com/c/second-annual-data-science-bowl
[mxnet]: https://www.kaggle.com/c/second-annual-data-science-bowl/forums/t/18079/end-to-end-deep-learning-tutorial-0-0392
[submit]: https://drive.google.com/a/nvidia.com/file/d/0B4INBpiK_--SNXdDYmltdVd2cGc/view
[valList]: https://drive.google.com/a/nvidia.com/file/d/0B4INBpiK_--SNldFajNlWXlrb1U/view
[Lenet]: https://drive.google.com/a/nvidia.com/file/d/0B4INBpiK_--SbnNqSFM4TlZBdDg/view
[preproc]: https://drive.google.com/file/d/0B4INBpiK_--Sbmh4TW1wcFYzUVU/view?usp=sharing
[pydicom]: http://www.pydicom.org/
[kagCardiac]: https://www.kaggle.com/c/second-annual-data-science-bowl/data
[deb]:	  https://github.com/NVIDIA/DIGITS/blob/master/docs/UbuntuInstall.md
[digits]: http://github.com/nvidia/digits