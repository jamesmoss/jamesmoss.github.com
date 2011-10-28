--- 
layout: post
title: Checkboxes in Chrome DevTools CSS inspector
published: true
meta: 
  dsq_thread_id: "404304014"
  _edit_last: "1"
tags: 
- Articles
type: post
status: publish
---
After being an avid Firefox fan for the past five years I’ve recently
decided to switch to Google Chrome as my main browser for both
development and general usage. It’s matured over the last few years to
become a great browser; fast, light on resources and with a brilliant
plugin system.

When using Firefox, the Firebug extension has become an
invaluable tool for debugging, diagnosing and investigating front end
HTML, Javascript and CSS issues. Chrome has an equivalent feature built
right into the browser and its great, except for one thing; The
checkboxes used to toggle properties in the CSS inspector are the on
wrong side. <!--more-->

## The problem

Here’s the CSS inspector in Firebug: 

![image]

Notice how the
button to toggle the CSS properties on and off is right next to the
property name itself. This close proximity makes it easy for the brain
to associate it to the height property. Now lets look at the equivalent
feature in Chrome developer tools: 

![image2] 

The button to toggle
the property is now a tiny checkbox placed way out on the right hand
side. The distance between the checkbox and the CSS property means that
its difficult to work out which checkbox applies to which property.
[Paul Fitts][] would be having a fit.

## The fix

After 2 minutes of playing around I realised the DevTools in Chrome are
actually plain old HTML, CSS and JavaScript. The CSS file is located at
`chrome-devtools://devtools/devTools.css`, I didn’t want to find this
file in the application package and directly edit it as my changes would
get overwritten on each upgrade. 

I started looking into plugins such as
[Stylish][] which let you inject custom CSS in any page you like.
However Chrome plugins are only loaded in pages using `http://`, `https://`
or `ftp://` protocols (and `file://`, if given permission by the user).
Eventually I came across the `Custom.css` which is Chrome’s equivalent to
Firefox’s `userContent.css`. `Custom.css` gets injected to all pages in
Chrome, even the extension management page, user preferences and of
course DevTools.

## Updating Custom.CSS

On OS X you can find your `Custom.css` file in
`~/Library/Google/Chrome/Default/User StyleSheets/`. If that folder is
empty just create the file yourself. I don’t use Windows but I’m sure
the file will be in a similar place. Place the following CSS in the file
and save.

<script src="https://gist.github.com/1074366.js?file=Custom.css"></script>
That’s all there is to it. You don’t even need to restart Chrome. 

I’m not sure if this will ever get properly fixed. It’s been [raised as an
issue][] in the Chromium project but it’s been marked as an external
dependancy issue within the WebKit engine. The WebKit team don’t seem to
be in any hurry to fix it either, it’s been sitting as [an issue in
their bug tracker][] for over a year with no real activity.

  [image]: http://jamesmoss.co.uk/wp-content/uploads/2011/07/css-inspector-firebug.png "css-inspector-firebug"
  [image2]: http://jamesmoss.co.uk/wp-content/uploads/2011/07/css-inspector-chrome.png
  [Paul Fitts]: http://en.wikipedia.org/wiki/Fitts's_law "Fitts's Law"
  [Stylish]: https://chrome.google.com/webstore/detail/fjnbnpbmkenffdnngjfgmeleoegfcffe
  [raised as an issue]: http://code.google.com/p/chromium/issues/detail?id=66628
  [an issue in their bug tracker]: https://bugs.webkit.org/show_bug.cgi?id=37770

