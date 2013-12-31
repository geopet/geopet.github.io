---
layout: post
title: "Zsh and Octopress: A Rake Globbing Challenge"
date: 2013-12-30 16:33:57 -0700
comments: true
categories: [tips, zsh, octopress, globbing, rake]
published: false
---
_It doesn't go without notice that a significant number of my posts have been about how to improve on the engine that I use to publish this blog. Keeping with this theme, I am writing two short posts on my experience of getting Octopress up to speed for the coming year._

In the second installment about my attempt to get Octopress updated for the new year, I wanted to talk shortly about how my change to Zsh affected my workflow. <!-- more -->

Octopress has some nice rake features that allow you to create new posts and publish quickly. In my previous post I talked about how I needed to introduce binstubs or use `bundle exec` to run rake properly.

This past year I decided to make [Zsh](http://www.zsh.org/) my default shell, moving away from Bash after a career of use. After getting past the loss of gemsets I ran: `% bin/rake new_post['My Awesome Title']` and got `zsh: no matches found: new_post[My Awesome Title]` in response.

{% pullquote %}
With a little bit of internetting I found that this was a [well understood issue](https://github.com/imathis/octopress/issues/117). [This one comment](https://github.com/imathis/octopress/issues/117#issuecomment-3707975) in the issue thread really covers the bases. {" What appears to be the case is that this isn't as much an Octopress issue as it is more of a Rake issue. And it isn't so much of a Rake issue as it is a Zsh globbing issue. "}
{% endpullquote %}

If you're like me you cocked your head to one side and wondered what exactly globbing was and why it would be affecting Rake tasks.

One of my favorite features in Zsh is its ability to autocomplete so much. For example if I want to list the files in my directory I can do:

```bash
% l
total 168
drwxr-xr-x  31 geopet  staff   1054 Dec 30 16:22 .
drwx------@ 32 geopet  staff   1088 Dec 26 07:57 ..
drwxr-xr-x   3 geopet  staff    102 Dec 30 15:02 .bundle
-rw-rw-rw-   1 geopet  staff    379 Jul 27 23:49 .editorconfig
drwxr-xr-x  18 geopet  staff    612 Dec 30 17:21 .git
-rw-rw-rw-   1 geopet  staff     12 Jul 27 23:49 .gitattributes
-rw-rw-rw-   1 geopet  staff    168 Dec 30 16:22 .gitignore
...
```

But with Zsh I can do even more interesting things. Like this:

```bash
% l G*
-rw-r--r--  1 geopet  staff   498 Dec 30 11:33 Gemfile
-rw-r--r--  1 geopet  staff  1533 Dec 30 12:21 Gemfile.lock
```

Or if I hit `<tab>` after typing `l G*` Zsh would complete the line with only the Gemfile and Gemfile.lock so I would end up with:

``` bash
% l Gemfile Gemfile.lock
```

It turns out that globbing is [the reason](http://zsh.sourceforge.net/Intro/intro_2.html) why I can do this in Zsh.

So Zsh globbing is essentially using regular expressions to do things like filename generation. Further, as the issue comment above mentions, [Zsh Filename Generation](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Filename-Generation) handles unquoted square brackets `[` and `]` as pattern generators. So when Zsh sees something like `bin/rake new_post['My Awesome Title']` it sees that first square bracket as a pattern generator and then freaks out when it isn't properly handled.

So cool, right?!

Well the long and the short of it is that one solution[^more solutions] when you're faced with this error using Octopress and Zsh is that you can run `bin/rake new_post` without arguments. At this point you get an input prompt and you can add your title.

```
% bin/rake new_post
Enter a title for your post:
```

While it was a long way to get here, I sure get a kick out of seeing how everything interacts, don't you?

[^more solutions]: See the [issue comments](https://github.com/imathis/octopress/issues/117) for more solutions. I chose this one for the simplicity of it all.