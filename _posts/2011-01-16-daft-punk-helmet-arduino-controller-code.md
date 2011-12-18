--- 
layout: post
title: Daft Punk helmet Arduino controller code
published: true
meta: 
  dsq_thread_id: "404303967"
  _edit_last: "1"
  _wp_old_slug: ""
tags: 
- arduino
- Articles
- daft punk
type: post
status: publish
---
Now and then it’s nice to step away from web development and work on a
project in [meatspace][]. Last year I was lucky enough to help the super
talented [Harrison Krix][] program the lights for his Guy Manuel [Daft
Punk][] helmet. He was midway through the project and had the
electronics nailed down but programming the [Arduino][] board wasn’t his
speciality so he got in contact with me after seeing [my Guy Man
helmet][] in action. I updated my original code (which used a
[Rainbowduino][]) to use Harrison’s Arduino setup, here it is in action:

<object classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000" width="480" height="385" codebase="http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=6,0,40,0"><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><param name="src" value="http://www.youtube.com/v/VDtRCbOoTGA?fs=1&amp;hl=en_US&amp;rel=0"></param><param name="allowfullscreen" value="true"></param><embed type="application/x-shockwave-flash" width="480" height="385" src="http://www.youtube.com/v/VDtRCbOoTGA?fs=1&amp;hl=en_US&amp;rel=0" allowscriptaccess="always" allowfullscreen="true"></embed></object>

Much better than my helmet for sure. I’ve had a few emails recently
asking for the source code for this. I’ve chatted with Harrison and he’s
happy to make it public so here it is: 

[DOWNLOAD][]
*(Note: requires
Arduino Potentiometer library which can be found [here][])*[][] 

It’s
released under an MIT license so feel free to do what you want with it
but make sure you include the license and original attribution if you do
decide to re-distribute it. 

Unfortunately I don’t have the time to write
up a big tutorial on how to use it at the moment or exactly how it
works, however the code is fairly well commented so unless you’re a
complete newbie you should be able to understand what’s going on. I’ll
try to answer any questions if you leave them in the comments. I’d also
like to state I’m by no means an Arduino expert so there may be better
or faster ways of doing things in the code which I’m not aware of, but
it all works. The electronics are detailed over on [Harrison’s blog][]
if you’re not already familiar with them.

  [meatspace]: http://en.wikipedia.org/wiki/Real_life
  [Harrison Krix]: http://volpinprops.blogspot.com/
  [Daft Punk]: http://en.wikipedia.org/wiki/Daft_Punk
  [Arduino]: http://www.arduino.cc/
  [my Guy Man helmet]: http://www.youtube.com/watch?v=TateK_wKyao
  [Rainbowduino]: http://www.seeedstudio.com/depot/rainbowduino-led-driver-platform-plug-and-shine-p-371.html
  [DOWNLOAD]: https://github.com/jamesmoss/guy-manuel-helmet-led-controller/zipball/master
  [here]: http://www.arduino.cc/playground/Code/Potentiometer
  []: /src/Guy_Manual_Helmet_LED.zip
  [Harrison’s blog]: http://volpinprops.blogspot.com/2010/07/daft-punk-final.html