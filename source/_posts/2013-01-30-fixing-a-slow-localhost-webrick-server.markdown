---
layout: post
title: "Fixing a Slow Localhost Webrick Server"
date: 2013-01-30 23:16
comments: false
categories: [ruby, rails, webrick, fix, localhost]
---
For the longest time I could not get Webrick to work for me. It would boot up with `rails s` but would take several seconds for even the default landing page of a rails app to load. It was terrible.

I resorted to using [Thin](http://code.macournoyer.com/thin/) as my default browser by making sure it was in all my Gem files, but I still wanted to figure out why Webrick simply wouldn't work for me. (Truth is, Thin is a better web server, but I still wanted to get Webrick to work for me.)

Searching for "webrick slow" brought up a possible solution via [Stack Overflow](http://stackoverflow.com/a/3465134/887078). Basically you change the `:DoNotReverseLookup` symbol in your global Webrick config from `nil` to `true`.

If you're on OS X Lion you'll find the Webrick configuration here:

`~/.rvm/rubies/ruby-1.9.3-p362/lib/ruby/1.9.1/webrick/config.rb`

I found the `:DoNotReverseLookup` configuration on line 36.

Once I made the change Webrick was screaming fast. I'm pretty happy about it.

I still haven't found the definitive reason why this problem is occurring, but at least this change appears to fix things for me.

----

Please note, depending on the version of Ruby you're running `ruby-1.9.3-p362` could be something different. Just as long as you're changing the `confg.rb` file in the `webrick/` directory, you should be fine.
