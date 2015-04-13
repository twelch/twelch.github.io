---
layout: post
title: "Arduino Project - Weather Station"
description: "Creating a simple home weather station with off the shelf hardware, web platforms, and Thingspeak"
category: articles
tags: [arduino, thingspeak, IoT, angular, d3, sass, gulp, sourcemaps]
comments: true
share: true
---

For the last couple months I've been prototyping a simple solution for collecting temperature and humidity data using an Arduino and visualizing it online in real-time.  It's been a fun experience from soldering connections and writing Arduino sketches in C to publishing data to the [Thingspeak IoT platform](https://thingspeak.com/) and designing a simple web interface for aggregating and visualizing the data.  It's still a work in progress but I'm ready to share some of my initial work.

All of the code including the Arduino Sketch and Angular app can be found on my [Github project](https://github.com/twelch/weather-station)

# Hardware

For the hardware I selected the [Arduino Uno R3](http://www.adafruit.com/products/500) microcontroller, [AM2302 temperature/humidity sensor](http://www.adafruit.com/product/393), and [Adafruit CC3000 Wifi Breakout Board](http://www.adafruit.com/product/1510).  With all the right parts I was able to put this together in a couple of hours.

<figure class="half">
  <a href="/images/posts/weatherstation/solder.jpg"><img src="/images/posts/weatherstation/solder.jpg"></a>
  <a href="/images/posts/weatherstation/connect.jpg"><img src="/images/posts/weatherstation/connect.jpg"></a>
  <figcaption>Soldering the Wifi chip connections and wiring everything up</figcaption>
</figure>

# Thinkspeak

The next step was to write [an Arduino Sketch](https://github.com/twelch/weather-station/blob/master/arduino/CC3000_weather.ino) to collect data from the sensors at a regular interval and send it to Thingspeak over WiFi.  For this I adapted an [older Adafruit tutorial](https://learn.adafruit.com/adafruit-cc3000-wifi-and-xively).

Thingspeak made it easy to setup a new channel to receive the sensor events for both temperature and humidity.  Once the sketch was setup I watched the data start to stream in.

# App Design

I then took some time to study the the aggregation features that the Thingspeak API provided and tested out the C3.js charting library.  I then put together a preliminary UI design with responsive mobile and dashboard views.

<figure class="half">
  <a href="/images/posts/weatherstation/ui.gif"><img src="/images/posts/weatherstation/ui.gif"></a>
  <figcaption>Desktop and mobile design comps</figcaption>
</figure>

# App Development

With the groundwork laid I'm moving forward with developing the dashboard prototype.  In addition to some tried and true front-end tools I wanted to incorporate some new ones.  The final list includes:

* Bower
* Gulp
* SASS + Sourcemaps
* Autoprefixer
* Bootstrap
* Angular JS
* Karma test runner

Stay tuned for the final results.


