---
layout: post
title: "Time Travelling With Vim"
modified:
categories: technical
excerpt: "Using vim to time travel"
tags: [technical, vim-tips, tips, vim]
image:
  feature:
date: 2015-05-30T12:06:18+05:30
comments: true
---

I usually work on many projects at a time and as a consequence, I tend to open many files. Having all
of my data backed in a VCS saves me the hassle of losing any committed data, but it's always possible to
shoot yourself in the foot by messing up the work tree; and this is where the editor of my choice -
the mighty and glorious - vim comes to the rescue. A little know fact - vim is a superhero - and
one of vim's superpowers is time travel - and not just any time travel - time travel on steroids.<br><br>
Other folks may call it persistent undo, but there's no fooling us! But being the humble superhero that vim
is, you need to tell vim to use time travel.<br><br>

First create an undodir for vim.
{% highlight bash %}
$ mkdir -p ~/.vim/undodir
{% endhighlight %}

Next you need to enable persistent undo by including the following lines in your vimrc:
{% highlight bash %}
set undofile
set undodir=~/.vim/undodir
{% endhighlight %}

And now even if you go on an editing rampage, vim will save the day. The next time, I shall introduce you
to vim's other superpower - the ability to use the multi-verse.
