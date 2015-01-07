---
layout: post
title: Currying in Haskell
category: haskell
---

I have heard about [currying](https://www.haskell.org/haskellwiki/Currying) my whole programming career, but I have never worked in a language that did currying. What exactly is currying? Let's take a look at an example.

{% highlight haskell %}
myAdd :: Int -> Int -> Int
myAdd x y = x + y
{% endhighlight %}

This code does exactly what you expect. It adds two numbers together.

{% highlight haskell %}
*Main> myAdd 1 2
3
*Main> (myAdd 1) 4
5
{% endhighlight %}

Let's break down each repl line.

* `myAdd 1 2` - This calls the `myAdd` function with two arguments just like we defined above. This call returns 3 as expected.
* `(myAdd 1) 4` - `(myAdd 1)` makes a call to `myAdd` with a single parameter. This ends up returning a partially applied function that when called adds `1` to any number. Calling `(myAdd 1) 4` ends up adding `1` and `4` together.

`(myAdd 1)` is a [partial application](https://www.haskell.org/haskellwiki/Partial_application) of the function `myAdd`. This is made possible because every function in Haskell is curried. This currying is hinted at in the `myAdd` function definition.

`myAdd :: Int -> Int -> Int` can also be written like `myAdd :: Int -> (Int -> Int)`. When calling `myAdd 1 2` we can really think of it as `(myAdd 1) 2`. As far as I understand it, that is really what Haskell does when calling `myAdd`.  This means under the covers Haskell really only deals with functions that take a single argument and return a single value. This makes it easy to partially apply any function. I am unsure if currying has any other benefits in Haskell.

What are the other benefits to currying?
