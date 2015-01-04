---
layout: post
title: Let vs Where in Haskell
category: haskell
---

In my [previous post]({% post_url 2015-01-03-Fibonacci-in-Haskell %}), I defined a couple of different ways to calculate [Fibonacci sequence](http://en.wikipedia.org/wiki/Fibonacci_number) numbers. Let's take another look at the `fibFast` function.

{% highlight haskell %}
fibFast :: Int -> Int
fibFast n =
  let fib = 0:1:zipWith (+) fib (tail fib)
  in fib!!n
{% endhighlight %}

We could have also defined this function with a `where`.

{% highlight haskell %}
fibFast2 :: Int -> Int
fibFast2 x = fib!!x
             where fib = 0:1:zipWith (+) fib (tail fib)
{% endhighlight %}

What's the difference between the two? In this case, I don't think much. I think the `where` version might read a little better.

There are differences between the two. `where` allows you to define variables at the end of the fuction. `where` variables are also visible to the entire function.

`let` is an expression. You can use a `let` anywhere you can use an expression. The variables defined in the `let` have a more narrow scope than the `where`. The `let` variables are only visible inside of the `let`.

There is a pretty good discussion of `where` vs `let` on the [offical Haskell wiki](https://www.haskell.org/haskellwiki/Let_vs._Where). I am not sure I understand all the different pros and cons of each yet, but maybe after a few more months learning Haskell it will click.

