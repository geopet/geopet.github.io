---
layout: post
title: "nvAlt Quick Tip"
date: 2011-09-20 08:00
comments: true
categories: [tips, nvAlt]
---

## Making Markdown Readable and Your Default File Type

So normally I don't write tips on productivity, but lately I have been
focusing more and more on workflow and I decided to start diving deeper
into things like Brett Terpstra's
[nvALT](http://brettterpstra.com/project/nvalt/), Smile's
[TextExpander](http://www.smilesoftware.com/TextExpander/), and Second
Gear's [Elements](http://www.secondgearsoftware.com/elements/) (ala [Mac
Power Users](http://macpowerusers.com/), [Back to
Work](http://5by5.tv/b2w) and [Merlin
Mann](http://www.merlinmann.com/)). This means you may see so more stuff
from me regarding cool tools like these.

But this is a quick tip. So here it is:

When I installed nvALT there were two pieces that threw me right away.
First, even after going into the preferences and changing "Read notes
from folder" to the folder that had all my Markdown notes it didn't
register any of them in the search.  The reason? I needed to change the
"Store and read notes on disk as" drop down from "Single Database" to
"Plain Text Files" and then I needed to add the file extension "md" to
the "Recognize individual files with attributes:" extensions. Check out
the screen capture below if this isn't quite making sense. (Also note
that there is a "+" in that preference window, next to the "-" symbol,
but it isn't showing right now in Lion.[^pe])

![](http://media.tumblr.com/tumblr_lqtxi4bkBW1qfn6cf.png)

The second item that started to bug me was that any new note/file that I
created was being created with the `.txt` extension instead of the `.md`
extension that I work in all the time now. Frankly, if I couldn't fix
this issue, I would have probably abandoned nvALT almost right away.
Fortunately, I found that by selecting "md" in the "Recognize individual
files with attributes:" list and then hitting the check mark, it bolded
it and my tests have showed that all my new files being made by nvALT
are now `.md` files.

With these two items out of the way I plan to seriously play with this
system.

If, by some freakish chance Brett Terpstra checks out this post, one
feature request that I would make right now is to allow for the use of
his [Marked](http://markedapp.com/) app for the preview instead of only
having the built in, but excellent, nvALT HTML preview. There's a good
chance that it is already a feature and I'm not aware of it. I'm loving
Marked, and if you're a Markdown person and not using it yet, you should
definitely check it out.

[^pe]:Many thanks to Eddie Smith at [Practically Efficient](http://www.practicallyefficient.com/2011/08/02/1l-byword-nvalt-simplenote/) for that helpful one-liner!
