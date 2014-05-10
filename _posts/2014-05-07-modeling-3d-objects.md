---
layout: post
title: "3D Modeling of Real Objects - VisualSFM"
description: "Using VisualSFM to model real world objects "
category: articles
tags: [VisualSFM, Python, Virtualbox, Photography]
comments: false
share: true
---

(header photo of sparse reconstruction)

I've been curious about 3D modeling of real-world objects for a while.  Before I discovered web mapping back at Portland State in '06, was putting together prototypes that took an SRTM Digital Elevation Model (DEM) covering Mt. Hood and produced and rendered a simple Triangular Irregular Network (TIN).  But how to produce that DEM yourself with commodity hardware?  Or better yet how to produce a 3D point cloud that represents a more complex 3D surface?

I spent some time this week on this question and  ct has been out and as I looked around last week at the evolving tech landscape, I see a number of And as I pulled my head up and looked around at the tech landscape over the last week, I see a lot of energy building set to be released over the next 6 months with the new Kinect poised for release, Primesense being bought by Apple, and their sensors being used in everything from startups like [Structure Sensor](http://structure.io) to Google's [Project Tango](https://www.google.com/atap/projecttango/).  

Itching to get my feet and without a Microsoft Kinect in hand, I was reacquainted by [Aaron Racicot](http://reprojected.com/) with a photogrammetry technique for 3D reconstruction called [Structure from Motion](http://en.wikipedia.org/wiki/Structure_from_motion).  In a nutshell it's estimating 3D structures from 2D images, producing a point cloud.  I remembered the Microsoft Photosynth project using this technique under the hood, and Aaron pointed me at the freely available VisualSFM tool.  I played with this tool off and on for about a week and I thought I'd share a few of my findings and tips to save others some time or headeaches.

## Getting up and running with VisualSFM in 2014

This is a great tool by Changchang Wu that saw a lot of development through 2012, but is starting to slow down now that Changchang has moved on to projects with Google.  Step 1 for me was installation on OSX, which I failed at.  But not for lack of trying!  The [available binary](https://dl.dropbox.com/u/3952686/VisualSFM.0.5.18-R2.zip) was out of date and I went down the rabbit hole of compiling myself and never made it back out.  To be fair, Changchang warned of this :)

{% highlight html %}
* The installation on Mac OSX requires more work.
You probably need to make small modifications to the code, or search for their Mac OSX ports.
{% endhighlight %}

Indeed.  For what it's worth, here's the direction I took if it's useful to others.  As it turns out XCode for OSX Mavericks doesn't include a GCC compiler, instead opting for the up-and-comer [clang](http://clang.llvm.org/).  I quickly [learned on the mailing list](https://groups.google.com/forum/#!msg/vsfm/wMB-Ya1WDgM/Kf1TFjuDxQEJ) that clang may simply not be able to compile VisualSFM or some of it's components.  The person in the email thread did have success on Mavericks by installing a gcc compiler using Macports.  Knowing Macports doesn't play nice with Homebrew, my package manager of choice, I opted to try and install gcc with homebrew.

{% highlight bash %}
brew install gcc49
{% endhighlight %}

After a few PATH adjustments I had gcc 4.9 up and running.  I started manually stepping through the OSX install scripts in [this Github project](https://github.com/iromu/vsfm-osx) manually, starting with using Homebrew to install dependencies.  And... things were compiling!  But alas I started running into issues at the linking stage.  I didn't have the time or patience to resolve this problem at the time, but it may be due to Homebrew ignoring my PATH settings and continuing to use the clang compiler to install base libraries while I used gcc for VisualSFM and the more direct dependencies.

## Back to Windows

So I bailed and opted for running VisualSFM in Windows through Virtualbox using a [modern.ie](http://modern.ie/en-us) VM and Changchang's binary executable.  What did I have to sacrifice by using a VM?  Using the GPU on my graphics card for feature detection, which speeds up calculations significantly.  Even adding Virtualbox Guest Additions and turning on 2D and 3D acceleration did not get VisualSFM to recognize or use the GPU in the Intel video card in my 2013 Macbook Pro.  A small sacrifice to make I decided.  Follow the instructions on [this FAQ page](http://ccwu.me/vsfm/doc.html#dep) under "CPU replacement for feature detection" to install a software equivalent.

I thought I was home free at this point, on too the fun stuff!  Instead of starting simple though, and taking photos of an object on my table, I decided I was going to go bigger.  Take a pile of photos from Flickr (licensed appropriately) of one of my favorite geologic landforms, Monkey Face, reconstruct this baby in 3D, and before I knew it I'd be printing some coffee table centerpieces for my climber friends for Christmas (I'm a little more than half serious ;)

(picture of Monkey Face photos in VisualSFM)

As it turns out, 3D reconstruction is a bit of an art for natural features.  Anything with lots of distinct features and edges, particularly buildings and man-made objects seems to work well.  More subtle objects need more images with smaller transition from one image to the next (lots of overlap).  What happens is VisualSFM ends up producing multiple models of different parts of your object, but doesn't have enough information to be able to connect the camera views together into one model.  So you end up with bits and pieces like this:

(2 images of pieces of Monkey Face with partial models.)

At first I didn't realize how to access the different models but with the "N-View 3D Points" screen open you can use the up and down arrow to switch between your different models.  Here's a few other tips for prepping photos:

* Make sure the exif information is included with your images.  The software needs information about your camera sensor and focal ratio.
* Lack of graphics memory can cause errors.  If in doubt, try reducing your photo resolution to 1200px or below.
* Try removing photos with a lot of direct sunlight and glare or with wildly different exposure.

## Back to Basics

Adding in photos of wood-turned pot. Added couple other objects into the scene to improve feature detection and matching between photos.

(photo of objects)

Ran the sparse reconstruction.  Excellent coverage in one model, lots of cameras all around.

(photo of sparse)

Ran dense reconstruction. Excellent coverage.  Cleaned up outliers, by hitting F1 and drawing rectangles around offending points.

(photo of dense with cleanup)

## Taking it further with Meshlab

## What's next

Three.JS Photosynth projects

  a while and the potential for mapping and modeling large-scale real-world objects.  Primesense and their   3D objects A few years ago I heard about the Microsoft Photosynth project which takes photos of a 


<figure>
	<a href="/images/posts/qgis-geojson-export.png"><img src="/images/posts/qgis-geojson-export.png"></a>
	<figcaption>GeoJSON export</figcaption>
</figure>