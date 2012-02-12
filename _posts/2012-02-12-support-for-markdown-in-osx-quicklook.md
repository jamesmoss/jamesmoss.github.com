---
title: Support for Markdown in OSX QuickLook
layout: post
---

QuickLook is an indispensable feature in OSX that I use many times every day. Highlight a file in Finder and tap space to see a preview of the file without having to open it in an editor. 

Recently I've been writing more and more documents in [Markdown](http://daringfireball.net/projects/markdown/) using [Mou](http://mouapp.com/) (including this blog post). Frustratingly, out of the box QuickLook doesn't support Markdown, you'll just see a larger version of the file icon.

There's an easy fix however in form of [Phil Toland's](http://fiatdev.com) [QLMarkdown](https://github.com/toland/qlmarkdown/). Installing it is easy:

1. Download the latest release by [clicking here](https://github.com/downloads/toland/qlmarkdown/QLMarkdown-1.2.1.zip).
2. Extract it somewhere temporarily and copy the `QLMarkdown.qlgenerator` file into `~/Library/QuickLook` (you may need to create this directory).
3. Relaunch Finder by alt+right-clicking on the icon in the dock and selecting the option at the bottom.

Boom. Markdown in QuickLook.