---
layout: post
title: "Python Dictionaries, PHP Associative Arrays and Python Objects"
date: 2012-09-25 20:47
comments: true
categories: [Python, PHP, Dictionaries, Associative Arrays, Objects]
---

If you read my previous post on [the challenge of education as a developer](http://blog.geoffpetrie.com/blog/2012/08/29/on-the-problems-of-education-in-a-developers-world/), you'll know about my interested in the Python language and syntax. I have had a reason to look at Python again recently and it's pretty amazing what I had forgotten about the language.

Now I'll admit that my understanding of object models and design patterns isn't the finest. But as I was going through my Python refresher I had a bit of an aha moment.

It was this line of code that struck me as pretty significant:

    return ";".join(["%s=%s" % (k, v) for k, v in params.items()])

This code came from the [Dive into Python](http://www.diveintopython.net/native_data_types/summary.html) website.

While it doesn't look remarkable on the surface, knowing that _everything in Python is an object_ (like Ruby and Javascript) you'll appreciate how cool that line of code is. Specifically the `";"` piece of it.

That `.join` method is called _by_ that semicolon. That's pretty cool.

To demonstrate the importance of this piece, I decided to see how I could actually produce the same results that line of code does in PHP.

So that you understand the whole piece to this, the `params` variable is actually a dictionary (aka, an associative array in PHP) created in a small module. The variable is:

    params = {"server":"gpetrie", \
              "database":"localhost", \
              "uid":"sa", \
              "pwd":"secret" \
             }

The output from `return ";".join(["%s=%s" % (k, v) for k, v in params.items()])` is:

    pwd=secret;database=localhost;uid=sa;server=gpetrie

So the piece we're going to focus on is how that last tuple is printed. You see that? `server=gpetrie`. There's no semicolon at the end of that. That's because the semicolon is the object calling the `.join` method.

How can I produce this same output using PHP and an associative array?

If I were to do something like this:

    $myParams = array("server"=>"gpetrie", 
                      "database"=>"localhost", 
                      "uid"=>"sa", 
                      "pwd"=>"secret");

to initialize the PHP script, and then follow it up with something like this:

    $str = "";
    
    foreach ($myParams as $k=>$v) {
      $str .= "$k:$v; "
    }  
    
    print_r($str);

We wouldn't get what we wanted. We'd get this:

    server:gpetrie; database:localhost; uid:sa; pwd:secret; 

That semicolon at the end. That's the problem.

So we try something a little more complex:
    
    $myParams = array("server"=>"gpetrie", 
                      "database"=>"localhost", 
                      "uid"=>"sa", 
                      "pwd"=>"secret");

    $arrayCount = count($myParams);
    $arrayKeys  = array_keys($myParams);

    for ($i=0; $i<$arrayCount; $i++) {
      $arrayKey = $arrayKeys[$i];
      $str .= $arrayKey.':'.$myParams[$arrayKey].';';
    }

    print_r($str);

But it doesn't work either. We get:

    server:gpetrie; database:localhost; uid:sa; pwd:secret; 

as our output.

That _semicolon_!!!

Now I could be way off here. There is likely a far more elegant solution to this than I did, but this is the solution I came up with to produce the same output as the one line from Python:
    
    $myParams = array("server"=>"gpetrie", 
                      "database"=>"localhost", 
                      "uid"=>"sa", 
                      "pwd"=>"secret");

    for ($i=0; $i<=$arrayCount--; $i++) {
      $arrayKey = $arrayKeys[$i];
      $str .= $arrayKey.':'.$myParams[$arrayKey].';';
      unset($myParams[$arrayKey]);
    }

    $str .= key($myParams).':'.$myParams[key($myParams)];
    
    print_r($str);

And now we get the result we want:

    server:gpetrie;database:localhost;uid:sa;pwd:secret

No semicolon at the end.

Now don't misunderstand the point of this. This isn't a Python versus PHP thing. This is just to show the interesting power of having everything as an object in Python and how much lighter your code can be because of it. Of course if you have a better solution to this than I do, please let me know. I'd love to see it.
