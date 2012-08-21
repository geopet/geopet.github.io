---
layout: post
title: "Helpful Linux Commands"
date: 2011-04-05 14:30
comments: false
categories: [command line, linux, tips]
---

I was asked to give a bunch of detail on a server that I use so that I could request permission to participate in migrating some of the web work I do onto a new CMS. The requests seemed fine, but the form provided no way of easily estimating the file numbers they requested. I used these linux commands to find the details I needed:

`find . -type f -name '*.php' | wc -l` gave me the number of files I had in the directory with .php file extensions.

`du /var/www/html/ -ch | grep total` gave me the total amount of disk space being used in the directory in "human readable" format.

`/sbin/ifconfig` gave me the ip address of the server the information was currently sitting on.

I had to look up the first one, I didn't know how to get down to that sort of granularity, but I think the others are worthy of documenting here in case someone finds some use in them.

I was then informed about this:

>Fun fact: "find -name -type" is way faster than "find -type -name" because it avoids doing a stat() call if the name doesn't match. stat() on a file that isn't already in RAM likely triggers a seek and can take beaucoup milliseconds.

Which is an awesome tip from a person who had been reading the blog.
