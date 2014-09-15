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

As an incentive to submit, we offered prizes from Mapbox, CartoDB, and ESRI as well as copies of the 2014 NACIS Atlas of Design for a variety of judged categories including best cartography, best use of open source data, and best anti-map map.  A People's Choice award was also offered where we allowed gallery viewers to vote for their favorits maps at the press of a button, the most popular winning the award on the conference Gala night.

# Conference Video

<figure>
	<a href="/images/posts/mapgallery/video-title.jpg" target="_window"><img src="/images/posts/mapgallery/video-title.jpg"></a>	
	<figcaption>Title slide</figcaption>
</figure>

For those attending the conference in person we wanted to create a more engaging experience that showed off the maps while connecting viewers directly with the authors.  Something that attendees could enjoy from the comfort of their chairs between talks and on the big screen in the OSGeo booth.  

We could put this together easy enough in Final Cut, but Justin Miller figured out an automated way of taking the JSON feed and stamping out stylized text onto high-res images using Imagemagick and some [shell script](https://github.com/pdxosgeo/foss4g-slideshow/blob/master/test.sh).  This was then bundled into a slideshow using Aperture along some title and sponsor slides I designed in Sketch.  Low-tech at its finest.

<figure>
	<a href="/images/posts/mapgallery/gallery-video.jpg" target="_window"><img src="/images/posts/mapgallery/gallery-video.jpg"></a>	
	<figcaption>Map slide with overlays</figcaption>
</figure>

We had so many more ideas but just didn't have the time to pull them off.  Overall I think the gallery was a success and people had great things to say. Big thanks to Lynnae Sutton, Tanya Haddad, and the gallery judges for contributing their energy and ideas as well as FOSS4G Nottingham for hosting the first map gallery last year and sharing their experiences.
