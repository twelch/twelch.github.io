---
layout: post
title: "Curating The FOSS4G Map Gallery"
description: "From planning to setup to execution"
category: articles
tags: [foss4g, map, gallery, php, javascript, python, mobile]
comments: false
share: true
---

It's been heads down the last month putting together this years [map gallery](http://2014.foss4g.org/map-gallery) for the FOSS4G international conference.  The gallery is a small part of a much bigger conference experience our Portland team pulled off this week, but a part that is near and dear to us, the maps! And the data and the stories that come with them.

88 map submissions came in from around the world forming a snapshot of what's possible with the data, tools, and design patterns that have emerged out of this community.  The gallery experience we wanted to create would let people casually peruse the maps and dive deeper at any point.

# Online Gallery

<figure>
	<a href="/images/posts/mapgallery/gallery-web.jpg" target="_window"><img src="/images/posts/mapgallery/gallery-web.jpg"></a>	
	<figcaption>Gallery front page</figcaption>
</figure>

We wanted the gallery to be a first-class experience on tablet and desktop, and at least a useable experience on phone as most people would be hearing about the gallery via Twitter and email.  This meant being able to quickly navigate through the maps with a swipe and one more touch to learn about the map/author and access the original work.

<figure>
	<a href="/images/posts/mapgallery/gallery-web2.jpg" target="_window"><img src="/images/posts/mapgallery/gallery-web2.jpg"></a>
	<figcaption>Single map view with details button</figcaption>
</figure>

<figure class="half">
	<a href="/images/posts/mapgallery/gallery-mobile.jpg"><img src="/images/posts/mapgallery/gallery-mobile.jpg"></a>
	<a href="/images/posts/mapgallery/gallery-mobile2.jpg"><img src="/images/posts/mapgallery/gallery-mobile2.jpg"></a>
	<figcaption>Mobile screens</figcaption>
</figure>

### The Software

The gallery backend was built on top of Wordpress using the [Ninja Forms API](http://ninjaforms.com/documentation/developer-api/functions/) and a [simple JSON feed](https://github.com/pdxosgeo/foss4g2014-wordpress/blob/master/themes/foss4g-theme/template-mapgalleryfeed.php).  The gallery front-end was created using the BlueImp Responsive Gallery, Packer, jQuery, and Bootstrap.  Add in some customization and a little bit of glue and we had a working gallery.

<figure>
	<a href="/images/posts/mapgallery/gallery-json.jpg" target="_window"><img src="/images/posts/mapgallery/gallery-json.jpg"></a>	
	<figcaption>Map JSON output</figcaption>
</figure>

### Voting

As an incentive to submit, we offered prizes from Mapbox, CartoDB, and ESRI for a variety of judged categories including best cartography, best use of open source data, and best anti-map map.  A People's Choice award was also offered where we allowed gallery viewers to vote for their favorits maps at the press of a button, the most popular winning the award on the conference Gala night.

# Conference Video

<figure>
	<a href="/images/posts/mapgallery/video-title.jpg" target="_window"><img src="/images/posts/mapgallery/video-title.jpg"></a>	
	<figcaption>Title slide</figcaption>
</figure>

For those attending the conference in person we wanted to create a more engaging experience and connect them directly with the map authors on Twitter.  I worked with Justin Miller to create a slideshow with multiple images per map that attendees could enjoy from the comfort of their chairs between talks and on the big screen in the OSGeo booth.  We considered using iMovie or Final Cut but we would have to overlay all of the map info by hand onto the images.  Instead, Justin cooked up an automated process for prepping the images and overlaying all of the text using Imagemagick, a little bit of [shell script](https://github.com/pdxosgeo/foss4g-slideshow/blob/master/test.sh), Node, and Aperture.  I used Sketch to design some additional title and sponsor slides.

<figure>
	<a href="/images/posts/mapgallery/gallery-video.jpg" target="_window"><img src="/images/posts/mapgallery/gallery-video.jpg"></a>	
	<figcaption>Map slide with overlays</figcaption>
</figure>
