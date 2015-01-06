---
layout: post
title: One Last Fibonacci Sequence
category: haskell
---

I have become obsessed with the [Fibonacci sequence](http://en.wikipedia.org/wiki/Fibonacci_number) in Haskell. Let's look at one last implementation I found on the ["Let vs. Where"](https://www.haskell.org/haskellwiki/Let_vs._Where) page and I swear I won't talk about Fibonacci any more.

{% highlight haskell %}
fibFast3 :: Int -> Int
fibFast3 = (map fib' [0 ..] !!)
           where
             fib' 0 = 0
             fib' 1 = 1
             fib' n = fibFast3 (n - 1) + fibFast3 (n - 2)
{% endhighlight %}

I like this implementation the best out of all the implementations so far. I don't think this implementation is the fastest, but I think it is a good mix between fast and readable. Let's break down the first line of this function.

`(map fib' [0 ..] !!)`

* [map](http://learnyouahaskell.com/higher-order-functions) is the traditional map function. `map` takes a function and a "list" and applies the function to the list. Keep in mind `map` is lazy and once a value has been caculated it remembers the result.
* `fib'` is our mapping function. `fib'` is defined just like the simple/slow Fibonacci definition from my first post about [Haskell Fibonacci]({% post_url 2015-01-03-Fibonacci-in-Haskell %}) numbers. This simple definition is what I like the most. It doesn't require any knowledge of Haskell to understand.
* `[0 ..]` is our lazy infinite number sequence.
* `!!` is our "get" function for lists. `[1, 0, 4] !! 0 => 1`

To make the whole thing work we need a little [currying](https://www.haskell.org/haskellwiki/Currying). That is why we have `()` around the whole expression. `(map fib' [0 ..] !!)` returns a function that when given a single integer will "get" that fibonacci number in our fibonacci sequence `map fib' [0..]`.

What do you think? Which one do you think reads the best?
