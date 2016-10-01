---
layout: post
title: A Year With Mapbox GL
description: making the switch to Mapbox GL in app dev
modified: 2016-09-15
category: articles
tags: [mapbox, react, animation, storytelling]
comments: false
share: true
---

It's been a year since I picked up the Mabox GL Javascript library.  Since then it's steadily improved and become stable across desktop and mobile.  It's now my mapping client of choice for most my projects.  Here's a quick summary of my tinkering over the last year.

* I started with designing and presenting some [compelling maps](http://dotsconnect.us/articles/happy-place/) with Studio
* I then started integrating Mapbox GL JS with React and Redux, creating a simple single-page [app template](https://reactmaps.firebaseapp.com) - published on [Github](https://github.com/twelch/react-mapbox-gl-seed).  Since then Uber has put out a more proper [React component](https://github.com/uber/react-map-gl) for GL JS that follows the style [proposed by tmcw](https://www.mapbox.com/blog/mapbox-gl-js-reactive/).
* Client work then took me down the path of storytelling and playing out choreographed scenes on a map, starting with [animating objects along a path](http://bl.ocks.org/twelch/18d53240f638d0c77cd4) and progressing to [layering in video and camera movement](http://bl.ocks.org/twelch/0ae8d02c78542a772401).
* Clustering support came to GL JS during the summer and I put that to use in a successful [social media campaign](/articles/workzonewtf/)
* Prototypes are fun to create but my clients want full-featured responsive apps with token-based auth, multi-tenancy, and internationalization.  So I took things further creating a lightweight [client](https://github.com/twelch/kit-client-react) and [server](https://github.com/twelch/kit-server-hapi) pair for quickly publishing map views.  I was able to take advantage of added GL JS support for switching languages and using Webpack.
* I found that my use cases for GL JS were growing increasingly complex, and at least once I found an [obscure bug](https://github.com/mapbox/mapbox-gl-js/issues/2926) that most would never hit.
