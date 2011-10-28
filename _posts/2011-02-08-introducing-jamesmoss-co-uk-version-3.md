--- 
layout: post
title: Introducing jamesmoss.co.uk version 3
published: true
meta: 
  dsq_thread_id: "413714374"
  _edit_last: "1"
  _wp_old_slug: ""
tags: 
- html5
- News
- photoshop
- redesign
type: post
status: publish
---
It's been a long time coming but this weekend I finally got round to finishing off my WordPress theme and, as you can see, have now got it live.  This new design also includes a drastic restructuring of the content within my site.  Previously the homepage was just a list of my most recent blog posts but I wanted it to speak to potential clients and employers so Ive introduced a new layout outlining who I am and what I do.  Hopefully it should give a clearer overview to new visitors who want to find out more.

Ive also made quite a few technical changes, here's an overview of the most important ones:
<ul>
	<li><strong>HTML5 markup</strong>.  I've used the <a href="http://nathanstaines.com/archive/starkers-html5-v3">Starkers</a> theme as a base and built on top of it with the <a href="http://borderleft.com/labs/">Toucan</a> reset stylesheet (I've added a few tweaks to handle the new HTML5 elements). I'm also using <a href="http://www.modernizr.com/">Modernizr</a> 1.6 to help older browsers to deal with the HTML5 pages properly. It's refreshing to use HTML5 after working with XHTML Strict for years, rather than worrying about ridiculous validation rules you can get on and make great looking sites.</li>
	<li><strong>Minified and combined my external CSS and JS to make the pages load a bit quicker</strong>.  Apache is also gzipping everything.  Currently my <a href="http://code.google.com/speed/page-speed/">Google page speed</a> ranking is 93, I could improve upon this but it quickly becomes a game of diminishing returns (No, Google I don't want to run every PNG on the site through pngcrush just to save 93 bytes) and the pages are generally loading below 500ms anyway which is acceptable.</li>
	<li><strong>Web fonts</strong><strong> - </strong>You'll notice the familiar (and probably overused) but brilliant Museo Sans for headings and titles.  This is courtesy of CSS3's powerful @font-face.</li>
</ul>
There's still a bit more work to do; I'd like to make my social media links more prominent by placing them on every page and introduce a jQuery powered image slider on the homepage but this will have to wait until I have another spare few hours.

Any feedback in the comments is greatly appreciated.
