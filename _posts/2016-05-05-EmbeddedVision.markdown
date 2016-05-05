---
layout: post
title:  "FP16 Training on Embedded"
date:   2016-05-05 08:00:00
categories: general
---

The [2016 Embedded Vision Summit][EVS] recently took place in the heart of Silicon Valley.  The summit started with a bang when Jeff Dean announced some impressive results using 8 bit deep learning models for inference.  For embedded and edge applications of deep learning models, 8 bit inference is a big deal.  A brief primer is that model size is reduced by four times since normally single precision uses 32 bits per value.  The power draw is significantly reduced as 8 bit arithmetic is nearly four times as fast and memory transfers can account for the majority of the power budget.   

![JeffDeanInference]({{ site.url }}/assets/jeffDeanEVS.jpg)
*Jeff Dean on the power and flexibility of deep learning* 

In this blog post, I'll present a complementary tutorial on training in 16 bits (specifically floating point 16 bits aka FP16) on the [Jetson TX1][TX1], which delivers nearly a 2x performance increase.  Notably, 16 bit arithmetic is supported natively on the TX1 and is an excellent feature preview for developing on the upcoming Pascal architecture, eg. the Supercomputer-in-a-Box [DGX-1][DGX].

First, grab the latest image for your TX1 through [Jetpack][jetpack].  NVIDIA provides the software free of charge and it's packed with goodies such as [VisionWorks][VS], [System Profiler][syspro], and [OpenCV4Tegra][opencvTegra].  If you choose to flash the image, this will displace your current system.  When prompted, install all the included packages.  The TX1 runs a full-fledge Linux kernel.  Start a terminal and check 

{% highlight bash %}
uname -a
{% endhighlight %}

returns a recent date.  Note, the power of the NVIDIA libraries allow high level API access to FP16 features.  Namely, [cuDNN][cuDNN] library version 3 introduced FP16 storage (activation values) and version 4 introduced arithmetic for convolutions.  Let's proceed by installing the relevant dependencies.

{% highlight bash %}
sudo apt-get update
sudo apt-get install aptitude screen git g++ cmake libboost-all-dev libgflags-dev libgoogle-glog-dev protobuf-compiler libprotobuf-dev bc libblas-dev libatlas-dev libhdf5-dev libleveldb-dev liblmdb-dev libsnappy-dev libatlas-base-dev python-numpy libgflags-dev libgoogle-glog-dev
{% endhighlight %}

Once those are installed, snag the FP16 enabled branch from the NVIDIA Caffe branch.

{% highlight bash %}
cd ~
git clone https://github.com/NVIDIA/caffe.git -b experimental/fp16 nvcaffe
{% endhighlight %}

Put this [makefile][nvmake] into the nvcaffe directory you've created and compile it.

{% highlight bash %}
cd nvcaffe
make -j 4
{% endhighlight %}

That's it.  Make sure your data is structured correctly, eg. [BVLC ImageNet recommendations][bvlcAlexnet].  Now, you can run a training as follows:

{% highlight bash %}
./build/tools/caffe_fp16 train --solver=models/bvlc_reference_caffenet/solver.prototxt -gpu 0
{% endhighlight %}

This will enable users to explore the high thoroughput world of FP16 training. One should carefully check convergence for their network, and techniques such as batch normalization will be valuable to scale values within the coverage in FP16.

Special thanks to Jeff Dean for suggesting the topic of this post and the [BVLC group][bvlcHome].  For more information, read the [Jetson TX1 whitepaper][whitepaper].

[cuDNN]: https://developer.nvidia.com/cudnn
[bvlcAlexnet]: https://github.com/BVLC/caffe/tree/master/examples/imagenet
[DGX]: http://www.nvidia.com/object/deep-learning-system.html
[TX1]: http://www.nvidia.com/object/jetson-tx1-module.html
[EVS]: http://www.embedded-vision.com/summit/agenda
[bvlcHome]: http://bvlc.eecs.berkeley.edu/
[jetpack]:https://developer.nvidia.com/embedded/jetpack
[syspro]:https://developer.nvidia.com/embedded/tegra-system-profiler
[VS]:https://developer.nvidia.com/embedded/visionworks
[opencvTegra]:http://docs.nvidia.com/gameworks/index.html#technologies/mobile/opencv_main.htm
[whitepaper]: https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwjigNPOmcLMAhVX72MKHZr5AAQQFggdMAA&url=https%3A%2F%2Fwww.nvidia.com%2Fcontent%2Ftegra%2Fembedded-systems%2Fpdf%2Fjetson_tx1_whitepaper.pdf&usg=AFQjCNFnm3jR1fIq2reER87RgJFwM5sDlw
[nvmake]: https://drive.google.com/file/d/0B4INBpiK_--SYmM3RFI1NFdXb0k/view?usp=sharing