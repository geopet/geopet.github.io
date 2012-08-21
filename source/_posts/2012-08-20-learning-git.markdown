---
layout: post
title: "Learning Git"
date: 2011-05-10 10:30
comments: true
categories: [Git]
---

##Introduction

For the record, much of this is unabashedly lifted from *Pro Git* book I
can't even remotely suggest that this content is original to me. Sure,
I've added my own two cents now and then, but do yourselves a favor and
read the first three chapters of [Pro Git](http://progit.org/book). In
fact, if any of this doesn't make sense, it is probably because I
haven't correctly paraphrased *Pro Git* and you should just consult the
book in that case.

One thing you'll definitively need to use Git locally is Git running on
your computer. There are lots of tutorials and ways to do it, I think
[this tutorial](http://progit.org/book/ch1-4.html) will work or you can
[just go to the source](http://git-scm.com/) and download the latest
stable release of Git.

The other item that you'll likely find useful in using Git as well as
for many other things, is a [Dropbox account](http://db.tt/eOrvceA). By
using Git in a Dropbox managed folder you get your own local repository
in the cloud. The Basic account type is free and comes with 2GB of
storage. That's probably plenty if you plan to mainly do textish style
file management. If it isn't enough space, hey, just get a paid account.
The service is awesome. The link that I give for the Dropbox account is
a referral link for me. It just me an extra 250MB of storage to my
account if you use it. If you'd rather not use that link then try
<http://www.dropbox.com>. I picked up this tip when I attended a
Webuquerque called *Getting With Git* that was presented by [Brian
Arnold](http://www.randomthink.net/).

Finally, this is not supposed to be a full explanation of how to use
Git. If you want that, as I said above, read the first few chapters of
[Pro Git](http://progit.org/book). The purpose of this is to touch on
basics of getting started and some of the more common commands. I used
Git while writing this document and I really enjoyed its simplicity.
From my perspective, this is worth your time to understand.

<!-- more -->

##Getting Started

After installation of Git on your system you need to configure Git with
identities for your machine:

    $ git config --global user.name "John Doe"
    $ git config --global user.email johndoe@example.com
    $ git config --global core.editor vim

This will give the repo info on who you are and what your editor of
choice is.

    $ git config --list
    user.name=Geoff Petrie
    user.email=gpetrie@email.com
    core.editor=vim

To get help:

    $ git help <verb>

eg,

    $ git help config
    $ git help commit
    $ git help branch
    $ git help tag

To start tracking an existing project locally go to the directory/folder
in your command line and enter this command:

    $ git init

This will create the .git subdirectory/subfolder, but nothing is
actually being tracked by Git yet. To begin tracking:

    $ git add *.php
    $ git add *.docx
    $ git add awesome_documentation.txt
    $ git commit -m "adding documents to be version controlled"

In that previous command you added all the .php files in the directory
you ran the `git init` command in, all the .docx (Word) files and a text
file called `awesome_documentation.txt`. Then you committed those
documents to your local repository with the `git commit` command.

Congratulations, you're now version controlling your work.

Another command you should know:

    $ git status

This will let you know whether you have a file(s) in the staging area
and ready to check in or something that has been tracked, has been
changed, but isn't in the staging area or you have untracked files in
the directory you ran `$ git init`.

    $ git diff

This command will show what you've changed but haven't staged yet.

    $ git commit

`git commit` commits your changes to your local repo. In this case it
will also launch your editor of choice where you will enter in a note
regarding the changes to the document you've made. When you save and
quit the editor your commit will be completed. To avoid launching your
editor add the `-m` flag:

    $ git commit -m "these changes will revolutionize the fashion industry."

Adding the `-a` flag to your commit will allow you to avoid the staging
area and commit files that have been modified immediately:

    $ git commit -a -m "this will commit straight into my repo, no staging required."

    $ git rm file.txt

Removes `file.txt` from your repo (and from your working directory).

    $ git rm --cached file.txt

Removes `file.txt` from your repo but *not* from your working directory.
(Good for when you may have accidentally added a bunch of files in your
repo that you didn't want to track, like complied files or admin text
files that you meant to put in your `.gitignore`.

    $ git mv file_from file_to

This is tied for my favorite command in Git. It renames the file and on
your next commit it renames it in your repo *and* your working
directory. So sexy. (My other favorite Git command is `$ git checkout -b
new_branch`, which I will get to in a moment.)

Here's how you can find out the changes that have taken place in your
repo:

    $ git log

    $ git log -p -2

The `-p -2` shows a diff and only the last two commits.

    $ git log --stat

Gives abbreviated stats for each commit.

The `--pretty` option allows you to use a prebuilt style or a style you
design to display the log. A pretty slick prebuilt is `oneline`:

    $ git log --pretty=oneline

Oooh. This is pretty awesome, too:

    $ git log --pretty=format:"%h - %an, %ar : %s"

    $ git log --since-2.weeks

This gives you only the changes that have happened in the last couple of
weeks.

The following commands allow you to commit a bunch of files, and then
add a file or two that you forgot to add in that last commit and add
them to that previous commit so that they all live happily ever after in
the same commit:

    $ git commit -m 'initial commit'
    $ git add forgotten_file
    $ git commit --amend

Sometimes you need to remove files from the staging area:

    $ git reset HEAD file_I_do_not_want.py

If you don't want to keep the changes to the file you have in the
staging area you can just revert the file back to the way it was in the
previous commit. *Be careful* this is not something you can undo:

    $ git checkout -- file_I_want_to_change_back.py

##Tags

Oh man. Now we're moving forward. Let's chat about *tagging*. Tagging is a
great place to mark a specific point in your version history as
important. This is perfect for a release point, i.e., v1.0.

To list the tags in Git you just fire off this command:

    $ git tag
    v0.9
    v1.0
    v1.1

To annotate a tag:

    $ git tag -a v1.4 -m 'my version 1.4 is the best thing ever.'

Here's how you see the data:

    $ git show v1.4

You can also tag a commit later in its life:

    $ git log --pretty=oneline
    9352eecf208721b29e73527219b64a5cbd175918 changes to april_notes, readded (with c
    9a4ccbebdcd934123831eb2ab4e1a6031d391c9a changes to iss53, newtest and april_not
    d8dddfe59b90fc80bc66571fe5364a40c0012503 Adding the newtest.markdown and complet

    $ git tag -a v1.1.0 9a4ccbe

Note you take the first part of that crazy list of numbers and letters
(the checksum) and add it to the end so that Git can identify which
commit you want to tag. God, isn't that simplicity awesome?

##Branching

Now, let's talk about *branching*.

For a more detailed discussion into branching, take a look at the
branching chapter in the [Git Pro
book](http://progit.org/book/ch3-1.html). For this discussion, I'm going
to show you the basic commands and what they do.

    $ git branch

Lists the branches already in your repository. Keep in mind that the
branch you'll likely find yourself in at first is your "master" branch.
This isn't necessarily the one you'll be spending the most of your time
in, but it is the default.

    $ git branch name_of_new_branch

This creates a new branch, eg, `$ git branch testing` will create the
branch "testing."

    $ git checkout testing

This changes the branch you are working on to the testing branch. The
master branch is the common branch that you would normally be working
in until you checkout another branch.

    $ git checkout -b new_branch

This is a shorthand command to create and checkout a new branch. *Very
handy.*

    $ git merge <branch name>

This command allows you to merge into your current branch another
branch's work.

    $ git branch -d <branch name>

The -d flag allows you to delete a branch.

Things get a little complex when you attempt to merge files that have
been changed in the same place in different branches. You'll likely get
something like this:

    $ git merge doc_test
    Auto-merging newtest.markdown
    CONFLICT (content): Merge conflict in newtest.markdown
    Automatic merge failed; fix conflicts and then commit the result.

Here you'll want to run `$ git status` to find out what issue is. You'll
see something like this:

    $ git status
    # On branch master
    # Changes to be committed:
    #
    #	new file:   testfile1.txt
    #	new file:   testfile2.md
    #	new file:   testfile3.php
    #
    # Unmerged paths:
    #   (use "git add/rm <file>..." as appropriate to mark resolution)
    #
    #	both modified:      newtest.markdown

For more information you can also run `$ git diff` to see what changes
are actually in play here.

    $ git mergetool

The mergetool will launch an appropriate visual merging tool that will
walk you through the conflicts.

One piece that I didn't cover earlier is how to revert back to a
different version of a file. To do this it requires a few different
commands.

First we want to check out the logs to see what changes we've committed.
After that we can use `diff` to see the difference in the files. Once
we're sure we are reverting to the correct version we use the `checkout`
command.

    $ git log
    commit 9e3b120796ed005f7542a73b20119870c8a966f7
    Author: Geoff Petrie <gpetrie@email.edu>
    Date:   Wed May 4 15:21:23 2011 -0600
    
        testing this commit after reverting to an older git_info.md file.
    
    commit cfd3c3980d5c04e976fbf7b3ab7a36e277b75259
    Author: Geoff Petrie <gpetrie@email.edu>
    Date:   Wed May 4 13:46:53 2011 -0600
    
        adding new commands, about to try reverting back a commit.
    
    commit 5407fc34f57f6dc6517a38194efa1a589f9a09ad
    Author: Geoff Petrie <gpetrie@email.edu>
    Date:   Wed May 4 13:17:13 2011 -0600
    
        a little change in the git doc
    
    commit 62d8d7e8fc12fcd0f1cfc170a1a847f622514e34
    Merge: c0ec484 6aa6a00
    Author: Geoff Petrie <gpetrie@email.edu>
    Date:   Wed May 4 13:12:59 2011 -0600

We now have a nice list of a few previous commits.

    git diff 5407fc34f57f6dc6517a38194efa1a589f9a09ad git_info.md 
    diff --git a/git_info.md b/git_info.md
    index 31f9fb0..d6d71fd 100644
    --- a/git_info.md
    +++ b/git_info.md
    @@ -248,3 +248,10 @@ The mergetool will launch an appropriate visual merging tool that will
     walk you through the conflicts.
     
     This concludes the basics of how to get started
    +
    +Other handy commands:
    +
    +    $ git log --abbrev-commit --pretty=oneline
    +
    +Provides an abbreviated SHA-1 of your git log, a nice thing to have when
    +you're trying to choose specific commits.

Now we have our diff in the file we're interested in reverting back.

    $ git checkout 5407fc34f57f6dc6517a38194efa1a589f9a09ad git_info.md

This brings the git info.md file into our current working directory from
here we can now make changes to that file or commit immediately. The
beauty? If we're unhappy with this, we can just revert back to the
previous commit through the same process.

A word of warning: You **can** lose data this way. Anything you've
committed to your repository you won't lose, but if you're working on a
file and then decide to mess with its version without committing, you'll
lose the work you've done. Good rule of thumb with version control: Just
commit your work.

This concludes the basics of how to get started with git. Something that
I haven't covered here is how to manage a repository that is remote like
on GitHub or some other server. I may get to this later, but that is
definitely outside the scope of this document. 

If you find something here that doesn't make sense or you believe is incorrect, please feel free to let me know.

##Command list:

I'm going to list a few commands here that you can use as a quick
reference. You may find this link to [Git
Documentation](http://git-scm.com/documentation) more useful. Scroll to
the bottom of that link for the command list.

    $ git config --list
    $ git init
    $ git add *.php
    $ git commit -m "adding documents to be version controlled"
    $ git commit -a -m "using the -a flag is a shortcut"
    $ git status
    $ git diff
    $ git rm file.txt
    $ git rm --cached file.txt
    $ git mv file_from file_to
    $ git log
    $ git log --pretty=oneline
    $ git tag -a v1.4 -m 'my version 1.4 is the best thing ever.'
    $ git branch name_of_new_branch
    $ git checkout -b new_branch
    $ git merge <branch name>
    $ git branch -d <branch name>
    $ git merge <branch name>
    $ git mergetool
    $ git checkout <SHA-1> <file name>

Another handy command:

    $ git log --abbrev-commit --pretty=oneline

Provides an abbreviated SHA-1 of your git log, a nice thing to have when
you're trying to choose specific commits.

