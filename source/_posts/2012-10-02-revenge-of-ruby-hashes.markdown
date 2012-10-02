---
layout: post
title: "Revenge of Ruby Hashes"
date: 2012-10-02 17:02
comments: false
categories: [Ruby, Hashes, Objects]
---

Because I can't seem to let this go, I continued to research the
challenge I was dealing with a [few days back](http://blog.geoffpetrie.com/blog/2012/09/25/the-ruby-hashes-case/)
where I was trying to get the [cool python trick](http://blog.geoffpetrie.com/blog/2012/09/25/python-dictionaries/)
to work with Ruby hashes.

After scrubbing the Ruby documentation a more carefully, it seems that
Ruby hashes and Python dictionaries are not entirely identical.  Most
importantly, Ruby hashes don't have the same string methods that Python
dictionaries do. Meaning: Ruby hashes and Python dictionaries, while
similar, may be more of an apples and oranges sort of comparison.

With this in mind, I tried to trim up the code I wrote the last time to
produce the same output. This is what I came up with:

{% codeblock The New Semi-Colon Goodness semicolon2.rb %}
hash = {"server"=>"gpetrie", "database"=>"localhost", "uid"=>"sa", "pwd"=>"secret"}
arr = Array.new

hash.each do |key, val|
  arr << "#{key}=#{val}"
end

puts arr.join("; ")
{% endcodeblock %}

What I'm doing here is forcing myself to work within the confines of the
initial premiss that the values are given to me in a hash. I convert the
hash to an array and then use the join method on the array to do what I
want to do to get the output that I want. _Semi-colon success achieved!_

I think we can generally agree that this is better than the option I
proposed previously:

{% codeblock The Old Semi-Colon Badness semicolon.rb %}
hash = {"server"=>"gpetrie", "database"=>"localhost", "uid"=>"sa", "pwd"=>"secret"}

hash.each do |key, val|
  if hash.length == 1
    print "#{key}=#{val}\n"
  else
    print "#{key}=#{val}; "
    hash.delete(key)
  end
end
{% endcodeblock %}

For my money, the new snippet is much more readable and is just a smidge
more compact. A win on all sides.

I probably won't be returning to this subject again in the near term
(unless I find out I'm totally wrong here), but expect more Ruby focused
conversation coming up regularly here while I work my way through the
language.
