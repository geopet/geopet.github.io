---
layout: post
title: "Git Tip: Use Prune to Update Local Repo Branches"
date: 2012-09-04 21:46
comments: false
categories: [git, tips, prune]
---

{% img center /images/git-prune.jpg [pruning the stale branches] %}

I have multiple places where I work and I use [Git](http://git-scm.com/) to support that. The general Git workflow I've adopted is similar to the one [Scott Chacon describes](http://scottchacon.com/2011/08/31/github-flow.html).

In Scott's post he explains that anything in `master` is deployable, and any time you want to work on something you branch from `master` with something descriptively named. This is what I want to talk about now.

I use this process of branching to keep my changes manageable. By naming my branches descriptively I know that if I'm building a new user profiling tool, and changing the css of a navigational piece and updating a SQL query in the same branch, then the commit isn't going to be terribly clean. Plus, now the branch has no meaning to me when I get feedback from a tester. This branch would make even less sense if I had someone else coding with me.

To keep branches meaningful I make a lot of branches off of `master`. I've come to the standard practice of pushing pretty much _any_ branch I'm working on, no matter how minor, to the remote. This makes it simple to `fetch` and `merge` on my dev server instance instead of scp'ing the work I've done to the server. The process is just feels a little crisper.

After the testers have given the thumbs up on the work and I do my final code review, I merge the branch to master, push it out to production and delete that feature/bugfix branch. All-in-all it is a generally good system.

But what inevitably happens is the dev server has a bunch of branches that are no longer useful and don't have a remote counterpart to them. It gets to be a bit of a mess when you run `git branch` and see a dozen old branches sitting there.

To fix this issue I found a great, quick command:

`git remote prune origin`

Where `origin` is the name of the remote.

[From the manual](http://www.kernel.org/pub/software/scm/git/docs/git-remote.html):

>**prune**

>`git remote prune [-n | --dry-run] <name>`

>Deletes all stale remote-tracking branches under `<name>`. These stale branches have already been removed from the remote repository referenced by `<name>`, but are still locally available in `"remotes/<name>"`.
    
>With `--dry-run` option, report what branches will be pruned, but do not actually prune them.

`prune` is one of those commands that you may not use very often, but it is nice to know it's there when you need it.

----

**Endnote:**

I found this particular [Stack Overflow](http://stackoverflow.com/a/3994587/887078) answer useful when I was looking for information on how to handle dead remote branches.

_Image "Four volunteers prune some plants that were growing over the trail." from [United States Government Work](http://www.flickr.com/photos/presidiosf/6209563606/)_