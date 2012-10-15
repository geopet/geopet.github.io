---
layout: post
title: "Git Tips: Tagging"
date: 2012-10-14 21:06
comments: false
categories: [Git, Tagging, Tips]
---

File this under the _I'm always referencing this, so I'm going to do a
quick post about it_ category.

Tagging in Git is super powerful and can save your butt. Here are a few
commands that I use often but never seem to remember.

**List** all your tags:

`git tag`

----

**Create** a tag:

`git tag -a v1.4`

----

**Push** tags:

`git push origin v1.4`

or

`git push origin --tags`

----

**Checkout** a tag:

`git checkout -b v1.4`

----

**Deleting** a tag

`git tag -d v1.4`

----

**Deleting** a _remote_ tag

`git push origin :v1.4`

----

**Search** for _specific_ tags:

`git tag -l 'v1.0.2'`

----

**See** tag _data_:

`git show v1.4`

----

**Retroactively** tag:

`git tag -a v1.4 <<checksum>>`

----

A couple of nice references on tagging:

[Git Basics - Tagging](http://git-scm.com/book/en/Git-Basics-Tagging)  
[Git Ready - Tagging](http://gitready.com/beginner/2009/02/03/tagging.html)

