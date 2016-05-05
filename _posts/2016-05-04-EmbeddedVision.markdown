---
layout: post
title:  "FP16 Training on Embedded"
date:   2016-05-05 15:00:00
categories: general
---

The [2016 Embedded Vision Summit][EVS] recently took place in the heart of Silicon Valley.  The summit started with a bang when Jeff Dean announced some impressive results using 8 bit deep learning models for inference.  For embedded and edge applications of deep learning models, inference is a big deal.  A brief primer is that model size is reduced by four times since single precision uses 32 bits per value.  The power draw is significantly reduced as 8 bit arithmetic is nearly four times as fast and memory transfers can account for the majority of the power budget. 

![JeffDeanInference]({{ site.url }}/assets/JeffDean8BitIntegerInference.jpg)

In this blog post, I'll present a complementary tutorial on training in 16 bits on the [Jetson TX1][TX1], which delivers nearly a 2x performance increase.  Notably, 16 bit arithmetic is supported natively on the TX1 and is an excellent feature preview for developing on the upcoming Pascal architecture, eg. the Supercomputer-in-a-Box [DGX-1][DGX].

First, grab the latest image for your TX1 through [Jetpack][jetpack].  NVIDIA provides the software free of charge and it's packed with goodies such as [VisionWorks][VS], [System Profiler][syspro], and [OpenCV4Tegra][opencvTegra].  If you choose to flash the image, this will displace your current system.  When prompted, install all the included packages.  The TX1 runs a full-fledge Linux kernel.  Start a terminal and check 

{% highlight bash %}
uname -a
{% endhighlight %}

returns a recent date.  Next, install the relevant dependencies.

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

That's it.  Now, you can run a training as follows:

{% highlight bash %}
./build/tools/caffe_fp16 train --solver=models/bvlc_reference_caffenet/solver.prototxt
{% endhighlight %}

Special thanks to Jeff Dean for suggesting the topic of this post and the [BVLC group][bvlcHome].

[TX1]: http://www.nvidia.com/object/jetson-tx1-module.html
[EVS]: http://www.embedded-vision.com/summit/agenda
[bvlcHome]: http://bvlc.eecs.berkeley.edu/
[jetpack]:https://developer.nvidia.com/embedded/jetpack
[syspro]:https://developer.nvidia.com/embedded/tegra-system-profiler
[VS]:https://developer.nvidia.com/embedded/visionworks
[OpenCV4Tegra]:http://docs.nvidia.com/gameworks/index.html#technologies/mobile/opencv_main.htm
[nvmake]: https://drive.google.com/file/d/0B4INBpiK_--SYmM3RFI1NFdXb0k/view?usp=sharing