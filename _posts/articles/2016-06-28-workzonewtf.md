---
layout: post
title: Crowdsourcing Policy Change in PDX
description: Using social networks to show that construction closures are endangering bikes and pedestrians
modified: 2016-06-28
category: articles
tags: [workzoneWTF, twitter, zapier, mapbox, google app script]
image:
  feature: posts/workzonewtf/closure.jpg
comments: true
share: true
---

Right now there are dozens of road closures impacting the pedestrian and bike networks in and around the boom town that is Portland.  They range from unnecessary inconveniences to downright dangerous, and they all are easily preventable.  

<figure class="third">
  <div class='twidget'>
    <blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr"><a href="https://twitter.com/hashtag/workzoneWTF?src=hash">#workzoneWTF</a> About 5100 block on SW Barbur northbound. Posted 45mph.  This was today 4/19/2015. No bike lane detour. <a href="https://t.co/NvuZ7FuvHU">pic.twitter.com/NvuZ7FuvHU</a></p>&mdash; Seth D. Alford (@setha45) <a href="https://twitter.com/setha45/status/722477768340996096">April 19, 2016</a></blockquote>
  </div>
  <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
</figure>

Yet, local transportation agencies and developers weren't convinced it was a big issue so a small group of us set out to capture just how bad things have gotten and push for the policy changes needed to address it.  We ran a short social media campaign over three months and with a little tech sauce we whipped up, we were able to aggregate hundreds of photo tweets from some dedicated individuals and submit them to City Hall as part of a proposed resolution to work zone closure requirements.  The resolution passed unanimously at the end of June!  Here's how we did it.

Oregon Walks and the Bicycle Transportation Alliance approached me with the social media campaign idea and I hatched a plan for a tech workflow that would:

- Make it simple for people to contribute images via Twitter and Instragram
- Collect contributions for review and approval (Zapier, Google Sheets, Google Apps Script)
- Publish approved contributions through a central website (Jekyll/Github Pages, Tabletop.JS, Mapbox GL JS)
- Be built entirely on free or low cost services

<figure>
  <a href="/images/posts/workzonewtf/workflow.jpg"><img style="margin: 0 auto; width:400px" src="/images/posts/workzonewtf/workflow.jpg"></a>
</figure>

In just a few short sprints we had something [up and running](http://vzwz.oregonwalks.org/).  Code available on [Github](https://github.com/pdxosgeo/workzonepdx)

<figure>
  <a href="/images/posts/workzonewtf/home-top.jpg"><img src="/images/posts/workzonewtf/home-top.jpg"></a>
</figure>
<figure>
  <a href="/images/posts/workzonewtf/home-map.jpg"><img src="/images/posts/workzonewtf/home-map.jpg"></a>
</figure>

Oregon Walks and BTA then went into action and got the word out to their networks.  The sightings started to [trickle in](https://twitter.com/search?q=%23workzonewtf&src=typd).

<figure class="third">
  <div class='twidget'>
    <blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Demonstrate need for work zone policies that provide safe route for walking &amp; biking! Snap photos &amp; tag <a href="https://twitter.com/hashtag/WorkZoneWTF?src=hash">#WorkZoneWTF</a> <a href="https://t.co/KW7hnZ1BUp">https://t.co/KW7hnZ1BUp</a></p>&mdash; BTA (@BTAOregon) <a href="https://twitter.com/BTAOregon/status/724987883942195200">April 26, 2016</a></blockquote>
  </div>
  <div class='twidget'>
    <blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Let&#39;s <a href="https://twitter.com/hashtag/crowdsource?src=hash">#crowdsource</a> work zone closures for <a href="https://twitter.com/OregonWalks">@OregonWalks</a> &amp; <a href="https://twitter.com/BTAOregon">@BTAOregon</a>! <a href="https://twitter.com/hashtag/VisionZero?src=hash">#VisionZero</a> <a href="https://twitter.com/hashtag/workzoneWTF?src=hash">#workzoneWTF</a> <a href="https://twitter.com/hashtag/ATSummit?src=hash">#ATSummit</a> <a href="https://t.co/WCIqnArIpM">https://t.co/WCIqnArIpM</a></p>&mdash; Ray Atkinson (@RayPlans) <a href="https://twitter.com/RayPlans/status/709854607745286144">March 15, 2016</a></blockquote>
  </div>
  <div class='twidget'>
    <blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Portlanders - when you see work zones with no pedestrian accommodation tweet it to <a href="https://twitter.com/hashtag/workzoneWTF?src=hash">#workzoneWTF</a> <a href="https://twitter.com/hashtag/ATSummit?src=hash">#ATSummit</a> <a href="https://t.co/KQWA0DOVvV">https://t.co/KQWA0DOVvV</a></p>&mdash; Evan Manvel (@evanmanvel) <a href="https://twitter.com/evanmanvel/status/709863386666766336">March 15, 2016</a></blockquote>
  </div>
</figure>

We [communicated directly](https://twitter.com/vzworkzones) with contributors to fill in gaps and provide encouragement.

<figure class="half">
  <div class='twidget'>
    <blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">.<a href="https://twitter.com/CLeonard46">@CLeonard46</a> thank you, we need more outer SE! Added to the map @ <a href="https://t.co/Ate6WwUgDP">https://t.co/Ate6WwUgDP</a></p>&mdash; VZ Work Zones (@vzworkzones) <a href="https://twitter.com/vzworkzones/status/730922748688535552">May 13, 2016</a></blockquote>
  </div>
  <div class='twidget'>
    <blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">.<a href="https://twitter.com/AdamHerstein">@AdamHerstein</a> What&#39;s the intersection here so we can place on the map at <a href="https://t.co/Ate6WwUgDP">https://t.co/Ate6WwUgDP</a>?  Thanks</p>&mdash; VZ Work Zones (@vzworkzones) <a href="https://twitter.com/vzworkzones/status/725785266196123649">April 28, 2016</a></blockquote>
  </div>
</figure>

Over time a wide swath of safety and accessibility issues were shared covering everything from large long-term building construction and roadway maintenance to temporary closures.  More than a few times both sides of the street would be closed, or car parking would be maintained while bike or pedestrian traffic would be blocked.  Far too often work signage, equipment, even port-a-potties would be placed unnecessarilyin the middle of bike lanes or sidewalks forcing people out of their lane of travel.

<figure class="third">
  <div class='twidget'>
    <blockquote class="twitter-tweet" data-lang="en"><p lang="und" dir="ltr"><a href="https://twitter.com/hashtag/sidewalkends?src=hash">#sidewalkends</a> <a href="https://twitter.com/hashtag/workzoneWTF?src=hash">#workzoneWTF</a> <a href="https://twitter.com/OregonWalks">@OregonWalks</a> <a href="https://t.co/hplgDCXdOJ">pic.twitter.com/hplgDCXdOJ</a></p>&mdash; Kari Schlosshauer (@galavantista) <a href="https://twitter.com/galavantista/status/725522059485286400">April 28, 2016</a></blockquote>
  </div>
  <div class='twidget'>  
    <blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">PBOT has both sidewalks on SE 11th closed at Caruthers. <a href="https://twitter.com/hashtag/WorkZoneWTF?src=hash">#WorkZoneWTF</a> <a href="https://t.co/VTmrAbkycC">pic.twitter.com/VTmrAbkycC</a></p>&mdash; Carl Larson (@LilBikesBigFun) <a href="https://twitter.com/LilBikesBigFun/status/742446668478484481">June 13, 2016</a></blockquote>
  </div>
  <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
</figure>

About halfway into the campaign, contributors started sharing examples of good closures, cases where the developer or the city took a little extra time to create a viable alternative for bikes and pedestrians or found a way to prevent a closure altogether.  New hashtags emerged including [#workzoneFTW](https://twitter.com/search?q=%23workzoneftw&src=typd) and [#workzoneWTG](https://twitter.com/search?q=%23workzonewtg&src=typd)!

<figure class="third">
  <div class='twidget'>
    <blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Bikes don&#39;t need much space to squeeze past construction. Way to go (WTG), <a href="https://twitter.com/PBOTinfo">@PBOTinfo</a> ! <a href="https://twitter.com/hashtag/workzoneWTG?src=hash">#workzoneWTG</a> not <a href="https://twitter.com/hashtag/workzoneWTF?src=hash">#workzoneWTF</a> <a href="https://t.co/99JIa9Du5U">pic.twitter.com/99JIa9Du5U</a></p>&mdash; Carl Larson (@LilBikesBigFun) <a href="https://twitter.com/LilBikesBigFun/status/718559751701790720">April 8, 2016</a></blockquote>
  </div>
  <div class='twidget'>
    <blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Thanks <a href="https://twitter.com/tvaarchitects">@tvaarchitects</a> for providing a ped path on Hawthorne at 31st! <a href="https://twitter.com/hashtag/workzoneFTW?src=hash">#workzoneFTW</a> not <a href="https://twitter.com/hashtag/workzonewtf?src=hash">#workzonewtf</a> is possible! <a href="https://t.co/gvp1IQSTpj">pic.twitter.com/gvp1IQSTpj</a></p>&mdash; Oregon Walks (@OregonWalks) <a href="https://twitter.com/OregonWalks/status/743895275652059136">June 17, 2016</a></blockquote>
  </div>
  <div class='twidget'>
    <blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">A two way protected bike lane through a work zone at NW 13th &amp; Jefferson. Not a <a href="https://twitter.com/hashtag/workzonewtf?src=hash">#workzonewtf</a> <a href="https://t.co/DeW8BCpHCE">pic.twitter.com/DeW8BCpHCE</a></p>&mdash; Nick Falbo (@nickfalbo) <a href="https://twitter.com/nickfalbo/status/733316703988252672">May 19, 2016</a></blockquote>
  </div>
</figure>

After 3 months, all of the contributions were reviewed and submitted to the city and presented in support of new guidelines proposed called [Safe Accommodation for Pedestrians and Cyclists In and Around Work Zones](https://www.portlandoregon.gov/transportation/article/579777).  The Oregonian [ran a story](http://www.oregonlive.com/commuting/index.ssf/2016/06/closing_sidewalks_bike_lanes_f.html) covering the issue.  

On June 30th a resolution was presented to the city council and passed 5-0.  The end right? No, just the beginning.  Now it's time to make sure the city and private developers follow through.

<figure class="half">
  <div class='twidget'>
    <blockquote class="twitter-tweet" data-conversation="none" data-lang="en"><p lang="en" dir="ltr">“<a href="https://twitter.com/twkovach">@twkovach</a>: This is a good policy <a href="https://t.co/z4i7qAWDL2">https://t.co/z4i7qAWDL2</a>” Portland social media campaign <a href="https://twitter.com/hashtag/WorkZoneWTF?src=hash">#WorkZoneWTF</a> leads to direct action.</p>&mdash; Marc Lefkowitz (@MarcLefkowitz) <a href="https://twitter.com/MarcLefkowitz/status/748568176070365184">June 30, 2016</a></blockquote>
  </div>
  <div class='twidget'>
    <blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">This is a clear <a href="https://twitter.com/hashtag/WorkZoneWTF?src=hash">#WorkZoneWTF</a>; how did <a href="https://twitter.com/PBOTinfo">@PBOTinfo</a> allow this? What happened to new rules?? <a href="https://t.co/camtU9g2MU">https://t.co/camtU9g2MU</a></p>&mdash; (((PJ))) (@__P__J) <a href="https://twitter.com/__P__J/status/755104355766837248">July 18, 2016</a></blockquote>
  </div>
</figure>
