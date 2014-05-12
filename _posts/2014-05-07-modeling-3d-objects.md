---
layout: post
title: "3D Modeling of Real Objects - VisualSFM"
description: "Using VisualSFM to model real world objects "
category: articles
tags: [VisualSFM, Python, Virtualbox, Photography]
image:
  feature: posts/visualsfm/monkey-feature.jpg
  credit: Laurel Fan.  Monkey Face
  creditlink: https://www.flickr.com/photos/laurelfan/304376867/in/photolist-sU1D2-2V6M7s-2V6N2Y-2V2obK-2V2oqi-6ZVejj-4x5ULw-6ZRf22-6ZRfoV-7YNdD-c7u4iG-c7u2NN-c7u37G-c7u3Ub-4x5UJA-4x5UsJ-4x1Jsc-4x5UGS-4x5UmL-4x5UAA-4x1K3K-4uB3dK-4uB3f6-4x1JFX-4x5UQb-4x5Ue9-4x1K1T-4x1L7i-4x5Uwu-4x1Joi-4x5U4o-4x1Jhv-4x5UbG-4x1KpB-4x1KCM-4x1Kig-4x1KmZ-4x5Vh7-4x5V8A-4x5V3o-4x5VdE-4x5Vbj-4x1JmM-4x5UgE-6r3pNq-6ZReJ4-4x1L2t-4x1KkR-2V2mZr-4uB3kc
comments: false
share: true
---

I've been curious about 3D modeling of real-world objects for a while.  Before I discovered GIS and web mapping back in '06, I was taking Digital Elevation Models (DEMs) and rendering Triangular Irregular Networks (TINs) with OpenGL.  But how to produce those elevation models yourself?  Or better yet how to produce a 3D point cloud that can represent a more complex 3D surface?

Fast forward 8 years into the smart phone and post-Microsoft Kinect era.  [InsideMaps](https://www.insidemaps.com/) is using standard smart phone cameras to model indoor spaces.  Primesense, the maker of the Kinect sensor has been bought by Apple, and their sensors are starting to show up in everything from [Structure Sensor](http://structure.io) to Google's [Project Tango](https://www.google.com/atap/projecttango/).  Things are moving quickly in this space.

Great use of commodity hardware, but you don't actually need it to do basic 3D modeling of objects I learned.  You just need a set of images of an object taken from different overlapping perspectives, and a [Structure from Motion] tool that turns them into a 3D point cloud.  A friend, Aaron Racicot pointed me at the freely available [VisualSFM](http://ccwu.me/vsfm/) tool for doing this.  The software itself is powerful, if a little bit unwieldy, as many academic tools are.  But through trial-and-error I ended up learning a lot about the technique.  Here's some of the steps I took to get setup and produce a workable final product, including relevant dead ends, hard to find instructions, and tips.

## Getting up and running with VisualSFM

### OSX

Step 1 was installation on OSX, which I failed at.  But not for lack of trying!  If you don't care for the details of this failure, skip ahead.  

The most recent [binary](https://dl.dropbox.com/u/3952686/VisualSFM.0.5.18-R2.zip) was built for Lion back in 2012 and wouldn't run on Mavericks so I went down the rabbit hole of compiling myself and never made it back out.  To be fair, Changchang warned of this :)

{% highlight html %}
* The installation on Mac OSX requires more work.
You probably need to make small modifications to the code.
{% endhighlight %}

Indeed.  Even more, it turns out XCode for OSX Mavericks now uses the up-and-coming clang compiler instead of GCC.  I quickly [learned on the mailing list](https://groups.google.com/forum/#!msg/vsfm/wMB-Ya1WDgM/Kf1TFjuDxQEJ) that others had hit a dead-end with clang.  The person in the email thread did have success by installing a gcc compiler using Macports.  Since I was well entrenched in using the Homebrew package manager, I opted for that direction.

{% highlight bash %}
brew install gcc49
{% endhighlight %}

After a few PATH adjustments so that the GCC compiler was being used, I started manually stepping through the OSX install scripts in [this Github project](https://github.com/iromu/vsfm-osx) manually, starting with using Homebrew to install dependencies.  And... things were compiling!  But alas I started running into issues at the linking stage.  I didn't have the time or patience to resolve this problem at the time, but it may be due to Homebrew ignoring my PATH settings and continuing to use the clang compiler to install base libraries while I used gcc for VisualSFM and the more direct dependencies.

### Back to Windows

So I bailed and opted for running VisualSFM in Windows with Virtualbox.  I used a [modern.ie](http://modern.ie/en-us) VM and Changchang's VisualSFM executable.  What did I have to sacrifice by using a VM?  Not being able to use the GPU on my graphics card for feature detection, which speeds up calculations significantly.  Even adding Virtualbox Guest Additions and turning on 2D and 3D acceleration did not get VisualSFM to recognize or use the GPU in the Intel video card in my 2013 Macbook Pro.  A small sacrifice to make I decided.  I followed the instructions on [this FAQ page](http://ccwu.me/vsfm/doc.html#dep) under "CPU replacement for feature detection" to install a software equivalent instead.

I thought I was home free at this point, on too the fun stuff!  Instead of starting simple, and taking photos of an object on my table, I decided I was going to go bigger.  Take a pile of photos from Flickr (licensed appropriately) of one of my favorite geologic landforms, Monkey Face, reconstruct this baby in 3D, and before I knew it I'd be printing some coffee table centerpieces for my climber friends for Christmas (I'm a little more than half serious ;)

(image of MF images in VisualSFM)

As it turns out, 3D reconstruction is a bit of an art for natural features.  Anything with lots of distinct features and edges, particularly buildings and man-made objects seem to reconstruct well.  More subtle objects need more images, and lots of overlap from one image to the next.  Without that there's not enough information to connect the camera views together into one model and you end up with fragments like this:

(2 images of pieces of Monkey Face with partial models.)

At first I didn't even realize Visual SFM was producing more than 1 model, but the log output mentioned a result of 5 models.  I learned you could switch between each of the different models from the "N-View 3D Points" screen by using the up and down arrow.  Scrolling your mouse wheel would increase or decrease the camera views so you could clearly see how each image was being placed in the 3D space and where the gaps were.

## Back to Basics

Adding in photos of wood-turned pot. Added couple other objects into the scene to improve feature detection and matching between photos.

<figure>
    <a href="/images/posts/visualsfm/woodpot-images.jpg"><img src="/images/posts/visualsfm/woodpot-images.jpg"></a>
    <figcaption>Set of 29 images</figcaption>
</figure>

Ran the sparse reconstruction.  Excellent coverage in one model, lots of cameras all around.

* Make sure the exif information is included with all of your images.  The software needs information about your camera sensor and focal ratio.
* Large images can cause errors.  If necessary, reduce your photo resolution to 1200px or below.
* Try removing photos that are off on their own, with a lot of direct sunlight and glare, or with wildly different exposure.  Then rerun your sparse reconstruction, see if you get fewer models.

<figure>
    <a href="/images/posts/visualsfm/woodpot-sparse.jpg"><img src="/images/posts/visualsfm/woodpot-sparse.jpg"></a>
    <figcaption>Sparse reconstruction.  27 of the 29 images were successfully used to make 1 model</figcaption>
</figure>

Ran dense reconstruction. Excellent coverage.  Cleaned up outliers, by hitting F1 and drawing rectangles around offending points.

<figure>
    <a href="/images/posts/visualsfm/woodpot-dense.jpg"><img src="/images/posts/visualsfm/woodpot-dense.jpg"></a>
    <figcaption>Final 3D point cloud from dense reconstruction (with some of the artifacts already removed)</figcaption>
</figure>

<figure>
    <a href="/images/posts/visualsfm/woodpot-dense-close.jpg"><img src="/images/posts/visualsfm/woodpot-dense-close.jpg"></a>
    <figcaption>Up close view of 3D point cloud</figcaption>
</figure>

## Taking it further with Meshlab

The point density produced through this technique is plenty high enough to produce a 3D model.

Link to tutorial, mention mesh import is error prone.

## What's next

Three.JS Photosynth projects
