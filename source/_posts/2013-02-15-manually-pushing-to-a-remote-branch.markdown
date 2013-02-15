---
layout: post
title: "Manually Pushing to a Remote Git Branch"
date: 2013-02-15 11:40
comments: false
categories: [git, branching]
---
If you have a heavy feature branch you may end up being in a place where your master local branch is actually another branch in your distributed repo. This can be confusing and cause challenges when pushing changes to your remote.

What you might see when you run `git remote show origin` is something like your Fetch URL and your Push URL are pointing to the same repo, and your local branch is properly configured for git pull, but git push is off.  It'll probably say something like:

`master pushes to master (local out of date)`

Now there are ways to configure push and use tracking, but this is how to properly push to a remote branch manually that you're not tracking locally:

`git push origin <local_branch_name>:<remote_branch_name>`

or:

`git push origin master:web_site`

This pushes your local branch `master` to the remote branch `web_site` on the remote repo `origin`.

And that's it!
