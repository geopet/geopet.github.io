---
layout: post
title: "Adding a CNAME to your Octopress Blog"
date: 2012-08-22 16:42
comments: false
categories: [octopress, dns, general]
---
This option isn't terribly well explained in the [Octopress documentation](http://octopress.org/docs/deploying/github/), and slightly confusing within the [Github](https://help.github.com/articles/setting-up-a-custom-domain-with-pages).

So that I could get _blog.geoffpetrie.com_ to work as my url to my Octopress blog hosted by Github at _geopet.github.com_, I needed to go to my current hosting service. In my case this is currently [Dreamhost](http://www.dreamhost.com/r.cgi?1197623).

Since I wasn't changing my top-level domain (TLD), I wanted to keep _geoffpetrie.com_ pointed at my hosting service, I wanted to add a subdomain, i.e., _blog_ to my domain name server (DNS) run by Dreamhost.

I went into the DNS configuration in the Dreamhost cpanel and added _blog_ as the **name/record**, _CNAME_ as the **type** and _geopet.github.com_ as the **value**.

This is the first step, and once the DNS is refreshed your new subdomain (in my case _blog.geoffpetrie.com_) will start pointing to a Github 404.

The next step is to add the CNAME to your Octopress _master_ branch. This is surprisingly simple, but not completely intuitive. In the top level of the _source_ branch, you want to use the command:

`echo 'blog.geoffpetrie.com' >> source/CNAME`

Of course you're going to use your own subdomain instead of _blog.geoffpetrie.com_. This command will create the CNAME file in your source directory with the url that you want to direct people to.

After this all that's needed is `rake generate` and `rake deploy`. (You may as well commit to your source branch after this.)

Wait a couple of minutes for things to work their way through DNS and Github's world and you'll be looking at your Octopress blog on your own domain.
