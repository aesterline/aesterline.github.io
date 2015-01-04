---
layout: post
title: Fibonacci Sequence in Haskell
---

I have finished the first 5 chapters in ["Learn You a Haskell for Great Good!"](http://learnyouahaskell.com/). I enjoy learning Haskell. Let's look at a couple of implementations of the [Fibonacci sequence](http://en.wikipedia.org/wiki/Fibonacci_number) in Haskell.

#### Fibonacci Function - Slow but Easy
{% highlight haskell %}
fibSlow :: Int -> Int
fibSlow 0 = 0
fibSlow 1 = 1
fibSlow n = fibSlow (n - 1) + fibSlow (n - 2)
{% endhighlight %}

Let's look at this example line by line.

1. `fibSlow :: Int -> Int` - Function declaration. This declares the name of the function and the input/output types.
2. `fibSlow 0 = 0` - [Haskell](https://www.haskell.org) has powerful [pattern matching](http://learnyouahaskell.com/syntax-in-functions). This line says when `fibSlow` is called with a zero return a zero.
3. `fibSlow 1 = 1` - Same as line 2, but when we see 1 we will return 1.
4. `fibSlow n = fibSlow (n - 1) + fibSlow (n - 2)` - Recursively define how to find fibonacci numbers bigger than 1.

This is an easy way to define a Fibonacci function, but it isn't very efficent. I tried calculating `fibSlow 1000` and I got tired of waiting for it to finish.

#### Fibonacci Function - Fast but Harder
{% highlight haskell %}
fibFast :: Int -> Int
fibFast n =
  let fib = 0:1:zipWith (+) fib (tail fib)
  in fib!!n
{% endhighlight %}

Let's take this example line by line.

1. `fibFast :: Int -> Int` - Function declaration just like the first example.
2. `fibFast n =` - Start of the function definition. Nothing really to see here.
3. `let fib = 0:1:zipWith (+) fib (tail fib)` - This is the meat of the function. It basically defines a lazy fibonacci sequence that starts at zero and goes on forever. This line is also a great example of the laziness of Haskell. This [stackoverflow](http://stackoverflow.com/questions/6273621/understanding-a-recursively-defined-list-fibs-in-terms-of-zipwith) post gives a great explanation of how this works in Haskell.
4. `in fib!!n` - Given the fibonacci sequence defined on line 3, get the nth item out of that sequence.

This function is much faster than the first. Here is my calculation of `fibFast 1000`.

{% highlight haskell %}
ghci> fibFast 1000
817770325994397771
{% endhighlight %}

I glossed over how `zipWith` and `!!` works, so let's look at some examples of their usage.

#### !! Examples
{% highlight haskell %}
ghci> [1,2,3] !! 1
2
ghci> [1,2,3] !! 0
1
{% endhighlight %}

#### zipWith Examples
{% highlight haskell %}
ghci> zipWith (+) [0,1,1] [1,1,2]
[1,2,3]
ghci> zipWith (-) [1,1,2] [0,1,1]
[1,0,1]
{% endhighlight %}

I am sure I will look back at this post in a few months and think I really didn't understand Haskell, but I feel like writing about it is starting to put me on the right path.


