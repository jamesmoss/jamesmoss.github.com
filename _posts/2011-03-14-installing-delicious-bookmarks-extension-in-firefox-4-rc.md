--- 
layout: post
title: Installing delicious bookmarks extension in Firefox 4 RC
published: true
meta: 
  dsq_thread_id: "404303984"
  _edit_last: "1"
tags: 
- delicious
- extension
- firefox
- Snippets
type: post
status: publish
---
*(Update 4th May: The recent Firefox 4.0.1 update has caused issues with
my original workaround, Ive now made changes below so that the plugin
continues working even after future updates)* 

I’m now using Firefox 4 RC
as my main browser; it’s stable, fast and the UI changes feel like a big
step forward. I haven’t had much problem getting my addons working but
the delicious bookmarking extension didn’t want to play ball. I use it
on a daily basis (check out my last few bookmarks over on the right hand
sidebar) so this was a real dealbreaker for me. 

After a bit of searching
on Google I couldn’t find a simple tutorial so I thought I’d put this
one together and help out anybody else looking for a solution to this
problem. Please note, this is for OSX but the process will be very
similar on Windows too. I’m also assuming you have upgraded from FF 3.6
and already had the delicious extension installed. If not you might need
to download/install it before taking the following steps.

1.  From the menus select Help \> Troubleshooting information
2.  On this new tab, near the top, you’ll see a field called Profile
    Directory. Click the button in the field to launch Finder (File
    Explorer for Windows).
3.  In the window which has popped up navigate to the extensions folder.
    Inside that should be another folder named
    “{2fa4ed95–0317–4c6a-a74c–5f3e3912c1f9}”. Inside this is a file
    called install.rdf
4.  Open install.rdf in any plain text editor.
5.  Around line 8 you should see some XML which looks like this:
    `em:maxVersion="4.0b3pre" />`
6.  Update this to `em:maxVersion="5.0" />` (See we changed “4.0b3pre”
    to “5.0”)
7.  Save the file and restart Firefox.
8.  Boom. The delicious extension will now work.

The toolbar icons look a little funky and don’t fit the new UI in FF4
but apart from that it seems to work perfectly and should keep you going
until delicious release their own update for FF4.