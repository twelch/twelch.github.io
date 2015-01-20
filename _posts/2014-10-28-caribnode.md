---
layout: post
title: "Reef Assessment in the Eastern Caribbean"
description: "Developing tools for coral reef monitoring and evaluation at multiple scales in the Eastern Caribbean"
category: articles
tags: [project, dataviz, geonode, openlayers 3, underscore, papaparse]
comments: false
share: true
---

In my [first post](/articles/collaboration-eastern-caribbean/) I described the increasingly crowded landscape of online geospatial systems in the Eastern Caribbean, and my plans to join the fray to design a GeoNode-based system for The Nature Conservancy in partnership with 6 participating Eastern Caribbean countries: Antigua and Barbuda, Dominica, Grenada, Saint Kitts and Nevis, Saint Lucia, and Saint Vincent and the Grenadines.

[CaribNode](http://caribnode.org) has now been released and I wanted to show off a little bit of what it can do.  We're taking a lean approach to this system and working to capture some value right away for the intended users before a lot of time and resources are spent building it out further.

# What It Can Do

First and foremost CaribNode is a data discovery tool, publishing access to aggregate regional datasets, both spatial and non-spatial, in standard forms.  Okay, nothing groundbreaking here...  

<figure>
    <a href="/images/posts/caribnode/caribnode1small.gif" target="_window"><img src="/images/posts/caribnode/caribnode1small.gif"></a>  
    <figcaption></figcaption>
</figure>

On top of that foundation is the ability to create and plug-in additional tools that take the published data and distill it down into simple and powerful data visualizations that managers at different scales need.

# Coral Reef Assessment Tool

The first tool we are creating is the Coral Reef Assessment Tool.  It's being designed to provide information at the regional, national, and the local level providing meaningful information to a variety of management roles in the region.  The information to be presented include a suite of biophysical, socio-economic, and management effectiveness indicators that characterize the status and trends of the marine environment, as well as the protected areas and communities within it.

<figure>
    <a href="/images/posts/caribnode/caribnode2small.gif" target="_window"><img src="/images/posts/caribnode/caribnode2small.gif"></a>  
    <figcaption></figcaption>
</figure>

# Next Steps

An early prototype of CaribNode was introduced last week to data managers for feedback at a [hands-on workshop](http://urisacaribbean2014.sched.org/event/75f52ad5e119b1b2b80e3fabab6665bc) hosted during the Caribbean URISA conference.  Key next steps including adding a site level view for individual protected areas and smoothing out some of the rough edges that you might have caught in the video.  The initial CaribNode prototype will be released in Decemeber 2014 and will continue to evolve over the next year as indicator datasets continue to be collected in each country.

# Technology

CaribNode makes use of a variety of modern tools including:

*   GeoNode 2.0 - Django, Geoserver, PostGIS, PyCSW, Boostrap
*   OpenLayers 3 - report visualizations
*   PapaParse - indicator data processing
*   Underscore JS - data manipulation and templates
*   Grunt/Bower - app setup and deployment

Code is available on GitHub at:
[https://github.com/twelch/caribnode](https://github.com/twelch/caribnode)

Developers will notice this is a fairly lightweight front-end, opting not to use heavy MVC type libraries.  This is changing, the next release of GeoNode will use AngularJS.