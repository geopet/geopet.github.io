---
layout: post
title: "The Ruby Hashes Case"
date: 2012-09-25 23:55
comments: true
categories: [Ruby, Objects, Hashes]
---

Contrary to the date listed, the [previous post](http://blog.geoffpetrie.com/blog/2012/09/25/python-dictionaries/) about Python and dictionaries and PHP and associative arrays was written a few weeks back. I've since been spending more time with Ruby.

After posting that article about how tight the Python code was in order to build a string with just the right number of semicolons, I decided to see if I could do the same thing with Ruby.

This is the solution I came up with:

    hash = {"server"=>"gpetrie", "database"=>"localhost", "uid"=>"sa", "pwd"=>"secret"}

    hash.each do |key, val|
      if hash.length == 1
        print "#{key}=#{val}\n"
      else
        print "#{key}=#{val}; "
        hash.delete(key)
      end
    end

I think I'm missing something here that would make this code much tighter. This looks very similar to the PHP code that I wrote as the solution in my previous article. There's got to be a method that I'm not using that would allow me to dismiss the `delete` and the `hash.length` that I am using.  

If you have thoughts or suggestions, hit me up on [Twitter](https://twitter.com/geopet) and let me know.
