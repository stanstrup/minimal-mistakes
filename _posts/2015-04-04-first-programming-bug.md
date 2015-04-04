---
layout: post
title: "First Programming Bug"
modified: Sat Apr  4 20:44:37 IST 2015
categories: technical
excerpt: The first programming that I encountered with JS
tags: [technical, javascript, js, ECMA]
image:
  feature:
date: 2015-04-04T18:23:20+05:30
comments: true
---

> This article has been featured on this blog for the sole purpose of embarrassing the author, who incidentally is also the author of this post.

Prima facie, ECMAScript -- the most popular language of the world -- appears to be an innocuous, straightforward language; but once you start getting serious with it, it is only then that it will reveal its myriad idiosyncrasies. What is truly remarkable is the fact that despite the fact that many seasoned veterans have been confounded by this language, it has now become ubiquitous in the world of computers.
My first encounter with this language left me exasperated. I was fairly competent in C/C++ and in my hubris thought not much of this “petty scripting language”, and surely I was in for a surprise. Having spent a long 20 minutes on a comprehensive three page ECMAScript primer, I proceeded to write a simple program. The program was to subtract two numbers and return the result.

{% highlight javascript %}
function sub( a - b )
{
    return a-b;
}
{% endhighlight %}

A bit too simple for someone who has vanquished behemoths like C, so I increased the repertoire of this function. I recalled that the primer had a section on object literals, which seemed like a great feature to test. I modified the program to add abilities of subtraction and multiplication using an object literal.

{% highlight javascript %}
function calc(a,b)
{
    return
    {
           add: a+b,
           sub: a-b,
           mul: a*b
    }
}
{% endhighlight %}

After this ostensibly trivial change, I tried running the program but in vain, for, for every input, the computer adamantly spewed the same output: “undefined”. This was nothing out of the ordinary, and I proceeded with an error correction drill which was ingrained in my brain after all the hours of programming in C.  I checked for syntax errors - none.  Then I tried to narrow down the possibilities of error and commented out various portions of the code --- which as you can see was very easy.

{% highlight javascript %}
function calc(a,b)
{
    return
    {
           add: a+b,
        // sub
        // mul
    }
}
{% endhighlight %}

The program still did not budge. Ideally I would have turned to a debugger and tried out various sophisticated debugging techniques (read ‘stare at the program and plead for mercy’); but ECMAScript was an altogether new beast, I was at loss. So, with no solution in sight, I turned to my my final recourse - google. After a few hours of searching and reading thread after thread of solutions, I finally found the error. The correct code was:

{% highlight javascript %}
function calc(a,b)
{
    return {
           add: a+b,
    }
}
{% endhighlight %}

And viola, the bug was fixed. Yes, the difference between my original code and the correct code is not evident at first sight, but nevertheless, was significant. The placement of the brace matters in ECMAScript because, of something known as semicolon insertion performed by the ECMAScript engines. A statement like

{% highlight javascript %}
return
{
}

{% endhighlight %}
is translated into
{% highlight javascript %}
return undefined;
{
};
{% endhighlight %}

And so my program always produced “undefined” as its result.

This particular vignette taught me humility, and ever since then, I've never started writing a computer program in an alien language without spending sufficient time going through the documentation and specification of the language.

