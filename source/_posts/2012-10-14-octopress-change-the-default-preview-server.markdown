---
layout: post
title: "Octopress: Change the Default Preview Server"
date: 2012-10-14 21:27
comments: false
categories: [Octopress, Tips, Ruby, Servers]
---

Another quick tip for people using [Octopress](http://octopress.org/):

If you're running Octopress on Mac OSX you may be running into some real
performance issues when you run the `rake preview` command to check your
posts locally before you run the `rake deploy` to get things up and
running live. This is because, for whatever reason, the
[Webrick](http://en.wikipedia.org/wiki/WEBrick) server runs slowly on
XCode 4.2+. I haven't dived deep into finding a solution for this
because I found a nice fix.

First, run `gem install thin` from your command line.

This command will install the [Ruby Thin Server](http://code.macournoyer.com/thin/). This server is what I use
for my Rails testing as well and it works exactly the way I want it to.
(I have read many recommendations on using [Pow](http://pow.cx/) as
well, but I haven't spent the time looking into it so I can't personally
recommend it yet.)

The next step is to change your `Gemfile` located in the top directory
of your Octopress files.  Simply add `gem 'thin'` to the development
group and save the changes. 

The next time you run `rake preview` your blog on
<http://localhost:4000> should run smooth as silk.
