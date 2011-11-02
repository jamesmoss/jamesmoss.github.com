---
title: Blog redesign
layout: post
---

What you're looking at here is the new version of my blog. I've decided to pare back the design to make the content really stand out, focusing on clean typography, vertical rhythm and minimalism. There's one full post per page (no read more links!) and comments are only visible on the permalink pages.

## Under the hood

The changes aren't purely cosmetic. I've been using WordPress for the last few years, and it's served me well, but I've become increasingly unhappy with how complex it makes writing blog posts. The process and distractions of logging in, messing around with the HTML in a WYSIWYG editor (it *always*  needs manual fixing) and publishing it puts up a barrier which stops me from blogging as much as I'd like to.

## Dr Jekyll and Mr Hyde

To that end I've been looking for something a lot simpler. I started looking into writing something lightweight with [Silex](http://silex.sensiolabs.org/) but didn't have the time to build and test anything substantial.

In the end I came across [Jekyll](https://github.com/mojombo/jekyll), written in Ruby, which is a "blog-aware, static site generator". You feed it some content and a HTML layout and it combines the two, generating the final flat pages to be served to your visitors.

Jekyll uses Liquid for templating, the syntax is similar to Django Templates and Twig. A basic layout for a post looks like the the following:




Content can be written in Markdown, Textile or plain ole' HTML. A snippet of YAML Front Matter at the top of each post can set metadata such as categories or tags. I've decided to use Markdown, it generates clean semantic HTML with the least amount of effort. A range of importers makes migrating content from another blogging platform super easy.

I don't get to use Ruby as much as I'd like to so I'm hoping Jekyll will give me a chance to do some hacking, I've already thought of a few ideas for plugins.

## Code highlighting

I want to start using this blog to post more code snippets and review other open source projects. I've enabled [Pygments](http://pygments.org/) within Jekyll which automatically highlights my code snippets. I'm using the [monokai](http://www.monokai.nl/blog/2006/07/15/textmate-color-theme/) theme (as I do in my usual code editor) which contrasts well against the rest of the page:

{% highlight ruby %}
class Employee < Person
  def initialize(fname, lname, position)
    super(fname,lname)
    @position = position
  end
  def to_s
     super + ", #@position"
  end
  attr_writer :position
  def etype
     if @position == "CEO" || @position == "CFO"
         "executive"
     else
         "staff"
     end
  end
{% endhighlight %}

Pygments is brilliant. It's got support for all the popular languages (and some less popular ones). I particularly like how I can display shell commands:

{% highlight bash %}
$ chmod 664 myfile
$ ls -l myfile
$ grep -v apple fruitlist.txt
{% endhighlight %}

Finally I've added some `inline code styles` to make distinguishing them from the rest of the body text easier.

## Hosting

The beauty of having flat HTML files is that you can host your site [literally](http://www.instructables.com/id/ServDuino-Arduino-Webserver/) anywhere, no need to install and configure complex web servers (I'm looking at you Apache).



