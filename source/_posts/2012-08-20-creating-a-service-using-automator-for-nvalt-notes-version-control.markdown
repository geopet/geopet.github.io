---
layout: post
title: "Creating a Service Using Automator for nvALT Notes Version Control"
date: 2011-09-21 08:00
comments: false
categories: [nvAlt, Git, Service, Automator, OSX, tips]
---

## Introduction

I'm going to get a pretty nerdy here for a moment.

So I dove in and I'm now using
[nvALT](http://brettterpstra.com/project/nvalt/),
[Elements](http://www.secondgearsoftware.com/elements/) and
[Git](http://git-scm.com/) for my note taking needs. Aside from a few
minor hiccups, which I'll address in a later post, this is really
working nicely.

The one thing that I needed when I added nvALT and Elements to my note
taking workflow was the ability to easily continue version control with
Git. Before taking on this new process I was using Git in my notes
directory and I wasn't about to lose that option now.

But the ease which nvALT allows me to create new text files, and with
nvALT built to work better with [smaller
files](http://brettterpstra.com/break-up-your-text-documents/), I need
some way to get my version control under control.<a href="#fn:1"
id="fnref:1" title="see footnote" class="footnote">[1]</a>

Here's what my workflow was:

1. Work, notes, work, notes.
2. Work, notes, work, notes.
3. Look at the time.
4. *Damn! How long has it been since I last did a commit?*
5. cd to my notes directory.
6. Commit my notes to my repository.

It wasn't really precision based. Plus it had the added detriment of
taking me out of what I was doing to commit my notes.

What I did<a href="#fn:2" id="fnref:2" title="see footnote" class="footnote">[2]</a> was create a Bash script and then used Automator to create a
Service for it that I also applied a keyboard shortcut to. 

If you're still with me, here's how I did it:

## The Reveal

First<a href="#fn:3" id="fnref:3" title="see footnote" class="footnote">[3]</a>, create your Bash script.

I keep all my notes in one directory. This is the way that nvALT and, it
seems, Elements like to work. With some light taxonomy (ala [Merlin Mann
and Mac Power
Users](http://macpowerusers.com/2011/03/mpu-046-workflows-with-merlin-mann-ii/))
I have a reasonably good system in place. All my notes are in a
[Dropbox](http://db.tt/eOrvceA) subdirectory called "notes."

To get this to work I created a Bash script named `git_notes.sh` and put
this in it:

    #!/bin/bash

    cd /Users/username/Dropbox/notes/
    git add .
    git commit -m 'nvALT Service Commit'
    echo "* "`date`" nvALT Commit" >> /Users/username/Dropbox/notes/noteCommits`date "+%Y%m%d"`.md

Now, you'll see that this is redundant and probably a lot silly, but
this is what it does.

1. It makes sure that we'r in my notes directory using the absolute pathname.
2. It stages only the modified files to the repository.<a href="#fn:4" id="fnref:4" title="see footnote" class="footnote">[4]</a>
3. It commits those changes and uses a standard message for my Git
   log file.
4. The last line is where it gets a little silly, it appends to another
   file in the same Dropbox subdirectory with a message that also gives a
   human readable date/time. Why am I doing this? I don't know, maybe
   someday I'll set up something to parse it to get some analytics of when
   I do most of my commits for my notes file. 

But now that we have our Bash script. The rest is *trivial*.

First, we open [Automator](http://support.apple.com/kb/ht2488) and
select "Service" as our document type under the "Choose a type for your
document:"

{% img center /images/creating-a-service-01.png %}

Next, we're going to change the "Service receives" from the default
"text" to "no input". Leave the "in" "any application" as it is.

{% img center /images/creating-a-service-02.png %}

Penultimately, we click "Utilities" under the left-side "Library" dropdown and
then drag the "Run Shell Script" from the middle column over to the
right side.

{% img center /images/creating-a-service-03.png %}

Lastly, we enter in the location of the script in the workflow. It's a
good idea to use the absolute pathname here. In my case it was
`/Users/username/Dropbox/notes/git_notes.sh`.

Once you save you'll have a Service that will be available from any
of your application menus. Click on the Service and it will do a Git
commit of all the changes to that notes directory as well as update the
faux log file we've created for the day.

{% img center /images/creating-a-service-04.png %}

But I don't like to use the mouse/trackpad that much. So the final touch
to this is to create a keyboard shortcut in your System Preferences. Go
to `Applications > System Preferences > Keyboard`. Then choose "Keyboard
Shortcuts" and select "Services" from the left side. Your new Service
should be at the end of the Services listings. Just click the blank
space at the far end of the window and you should get a text input
field. You can use anything you want for your shortcut, but I chose
control-option-command-shift-s for mine to avoid any chance of a
keyboard conflict.

{% img center /images/creating-a-service-05.png %}

## Conclusion

So there you have it. A quick and dirty way to make sure that the notes
you're producing will be version controlled through Git. As a final
remark, I'll say that having version control has already paid off for
me.

I use multiple computers and I made the *huge* mistake of accidentally
deleting a bunch of files when a prompt popped up and I didn't read
exactly what it said. All of a sudden 20-some-odd notes of mine were
*gone*. But version control to the rescue! I *knew* I had just committed
to my repo before I had deleted the files and I was able to pull them
back from brink of deletion hell. But this was even easier than it could
have been because I had been using `git add .` instead of `git add -a`.
All it meant was that I needed to unstage the deleted files. It was
great and a perfect reason why doing something like this makes sense.

## Post Script

I should add that the use of a common/standard commit message is bad
practice. The reason I do this, instead of throwing a prompt so that I
can enter in a more detailed message, is that this is supposed to create
a workflow that won't interrupt what you're in the middle of but give
you the peace of mind that you've got things in a version controlled
environment. This *does not* prevent you from going to your notes
directory and doing a proper Git commit with a detailed message on what
you've done since your last commit. In fact, at the end of this
paragraph I'll be committing properly to say that this draft is
finished. And when I finish my review of the draft I'll commit again,
and message that it is ready for posting. After that, I'll probably do a
name change to the file (this is the taxonomy thing I mentioned before)
and then do another *proper* commit.

One last point: You may have noticed that you can easily change the Bash
script to point to any directory you want. Once you have the Service in
place, you can edit your `.sh` file whenever you please and have a
temporary keyboard shortcut for Git repo commits. I think that's kinda
cool.

<div class="footnotes">
<hr />
<ol>

<li id="fn:1">
<p>For example, I have already committed this post three times. <a href="#fnref:1" title="return to article" class="reversefootnote">&#160;&#8617;</a></p>
</li>

<li id="fn:2">
<p>My solution was to produce a quick and dirty Bash script
and then have it run through <a href="http://developer.apple.com/library/mac/#documentation/Darwin/Reference/ManPages/man1/launchctl.1.html">launchctl</a> on a regular basis. <a href="#fnref:2" title="return to article" class="reversefootnote">&#160;&#8617;</a></p>
</li>

<li id="fn:3">
<p>This tutorial assumes you have a local Git repo in place.
If you don&#8217;t have one and want to learn how, you can check out my
<a href="http://faceofgeoff.com/post/5383300462/learning-git">post</a> on the subject of Git. <a href="#fnref:3" title="return to article" class="reversefootnote">&#160;&#8617;</a></p>
</li>

<li id="fn:4">
<p>This is a key point because what I am <em>not</em> doing is
staging any files for <em>deletion</em> only modification. This means I won&#8217;t
worry about any files going away without my knowing. <a href="#fnref:4" title="return to article" class="reversefootnote">&#160;&#8617;</a></p>
</li>

</ol>
</div>

_I originally posted this tutorial on my Tumblr: [The Face of Geoff](http://faceofgeoff.com/post/10480335918/creating-a-service-using-automator-for-nvalt-notes)_
