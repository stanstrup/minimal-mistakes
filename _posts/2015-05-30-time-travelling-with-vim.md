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

I usually work on many projects at a time and as a consequence, I tend to open as many files as I
close at any given span of time. Having all of my data backed in a VCS saves me the hassle of losing
any data that has been committed to the system, but I can always shoot myself by messing up my work
tree and this is where the editor of my choice - the mighty and glorious - vim comes to my rescue.
One of vim's superpowers is time travel, and not just plain old time travel, time travel on
steroids.<br><br>
Vim might call it persistent undo, but there's no fooling us. To enable time travel, you need to
create an undodir for vim to use.<br><br>

{% highlight bash %}
$ mkdir -p ~/.vim/undodir
{% endhighlight %}

Next you need to enable time travel by editing vimrc and including the following lines:<br><br>

{% highlight bash %}
set undofile
set undodir=~/.vim/undodir
{% endhighlight %}

And now you can go on an editing rampage and never be afraid of losing anything. Which
is kind of a code nirvana.<br><br>
The next time, I shall talk about vim's other time travel superpower - multi-verse.<br><br>
