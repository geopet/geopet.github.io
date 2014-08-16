---
layout: post
title: "Analysis of Ottinger's Rules for Variable and Class Naming"
date: 2014-08-15 23:04:25 -0600
comments: true
categories: naming
---

Sections in Ottinger's *Rules for Variable and Class Naming*:  
* Use Intention-Revealing Names  
* Avoid Disinformation  
* Make Meaningful Distinctions  
* Use Pronounceable Names  
* Use Searchable Names  
* Avoid Encodings  
* Avoid Mental Mapping  
* Use Noun and Verb Phrases  
* Don't Be Cute  
* Pick One Word Per Concept  
* Don't Pun  
* Use Rich Name Sources  
* Make Context Meaningful

Naming is one of those things in programming that is always there. Tim Ottinger wrote [*Rules for Variable and Class Naming*](http://www.objectmentor.com/resources/articles/Naming.pdf) for Object Mentor in 1997. This is still considered one of the seminal articles on the topic of naming and programming. I thought it might be fun to give it a read an add my thoughts.

Let's get started.

Ottinger starts his paper with:

> An expressive name for a software object must be clear, precise, and small. This is a guide to better clarity, precision, and terseness in naming.

This focus on "terseness" immediately worries me. With autocompletion and IDEs, the size of the variable or class name is the last thing I'm going to worry about. But let's see where this heads.

## Use Intention-Revealing Names

> The problem isn't the simplicity of the code but the implicity of the code: the degree to which the context is not explicit in the code itself.

This is Ottinger's conclusion after looking at what appears to be a relatively simple Python sample. Ottinger's meaning is here is: *Even the simplest code needs to be clear in its intent.*

In Ottinger's example he takes the unexpressive names of the sample and modifies them to show the intent of the code. He takes his refactoring even further than name changing to introduce a new class using a name he had introduced in the previous refactoring. This new class adds an additional level of elegance and explicitness to the sample.

Something that started out as being difficult to understand, after some small changes, is significantly more clear.

<!-- more -->

## Avoid Disinformation

> A software author must avoid leaving false clues which obscure the meaning of code.

Some words mean different things to different people. Ottinger uses the word "list" as an example of something that could mean various things to various people. 

He argues that instead of `AccountList` perhaps use `AccountGroup` or even `BunchOfAccounts`.

Also, be careful using variables or classes whose names are both long and are only slightly different. For example, `XYZControllerForEfficientHandlingOfStrings` and `XYZControllerForEfficientStorageOfStrings`.

Amusingly, Ottinger warns us of using lowercase L's and uppercase o's in our naming as they can easily be misinterpreted as ones and zeros. Raise your hand if you've been bitten by this one before.

## Make Meaningful Distinctions

> If names must be different, then they should also mean something different.

This quote has a lot of meaning behind it. Consider the single responsibility principle. If you can't come up with a unique name for something, perhaps that is an indication that the code written with the name that you want to use could *also* be used for your current problem.

Ottinger warns us against adding noise words and number series in our naming simply to satisfy compilers. Creating variables like `string`, `string1`, `string2` add nothing to meaning. The same thing can be said about adding noise words like `Info` or `Data` to produce new classes like `ProductInfo` or `ProductData`.

"Noise words" are tricky for me to understand, though. I can see cases where `ProductInfo` and `ProductData` could be useful. But I feel that Ottinger's intent here is to warn off the use of these words if something more *explicit* can't be used. 

Furthermore, if you are creating a class called `ProductInfo`, perhaps it would be better to have an `info` method on the `Product` class. Then you could simply call `Product.info`.

## Use Pronounceable Names

This is a fairly self-explanatory section. Use variables and classes that you can say over the phone or in an in-person conversation.

## Use Searchable Names

Two outstanding quotes from this section:

> ... longer names trump shorter names, and any searchable name trumps a constant in code.

and

> My personal preference is that single-letter names can ONLY be used as **local** variables inside **short** methods.

I love these clear rules of thumb. Although I do worry over the use of single-letter variables in *any* place. I also have some challenges reconciling the idea that "longer names trump shorter names" but from before we saw that we should be "terse" in our naming.

Ultimately, for me, if a name is descriptive that should be the most important thing. If that name is short and descriptive, then that is fine. If it is long and descriptive then that, too, is just fine.

## Avoid Encodings

Ottinger brings this section to a close with this quote:

> Modern languages don't need type encoding.

It's certainly worth reading this section and learning more about Hungarian Notation, but I won't spend any more time on this here.

## Avoid Mental Mapping

Don't force the reader of your code to translate what the variable means.

And how awesome is this quote?

> Smart is overrated. Clarity is king. The very smart must use their talent to write code that others are less likely to misunderstand.

## Use Noun and Verb Phrases

Create variables that allow for you to write code that reads like a sentence.

Ottinger recommends that if this sounds unimportant or difficult to grasp then you should see how difficult it is for you or your colleagues to use your class's API or how challenging it is to read the unit tests for your class.

Another interesting element to this section is the idea of creating methods or functions to make your class read better instead of having a list of overloaded class constructor parameters that wouldn't make sense if you saw the class being instantiated.

So instead of `Interest.new(30)` you could have something like `Interest.thirty_year_mortgage`.

## Don't Be Cute

I once named a major function to a class `parsenator`. Don't do this. 

Seriously, even if the developers who read your code are fans of *Phineas and Ferb*, no one wants to see that when they're trying to debug something that woke them up in the middle of the night.

## Pick One Word Per Concept

Frankly, this section wasn't completely clear to me. What I'm taking from this is the idea that you should pick a name and then stick with it. Be consistent with your interface.

While this may be tedious, the people who use your API will thank you.

## Don't Pun

Do not use the same name for different ideas. 

Ottinger uses the term "add" as an example. If you use the name "add" in one class to be the summing of numbers and then use "add" in another class to concatenate a list, you are essentially muddying the clarity of what that term means in your system.

Use different names for different actions or things.

## Use Rich Name Sources

Use names that identify the patterns, algorithms or math terms you are using if you are working at a low level in the code. I.e., use *solution domain names*. It is better to be clear what the intent of your code is to the developer who will be maintaining it rather than the customer you have written the code for.

At a higher level, though, use *problem domain names*. Using the problem or business domain names makes the intent clear when you are interacting on that level. Is it easier to understand `Game.target.find(23)` or `Game.enemy_hit_in_quadant?(23)`?

## Make Context Meaningful

There are two items to walk away with from this section.

First, most names are not meaningful unto themselves. Use classes, methods and namespaces to help your readers better understand what your intent is.

Second, do not go around prefixing all of your classes with the problem domain abbreviations. 

If all your classes start with `BAZ`, not only does that not add anything to the clarity of your intent, it also works against autocompletion of your editors and IDEs.

## Conclusion

Ottinger's paper is exceptional. While I have enjoyed writing this analysis, I am certain that I am missing nuance that is there.

I encourage you to sit down and read through the paper for yourself. At best it'll take you just a short time longer to read it than it did to read this article here.

I'm writing this analysis as a learning tool. Please reach out to me if you find anything you want to discuss in greater depth or you have found something incorrect here.
