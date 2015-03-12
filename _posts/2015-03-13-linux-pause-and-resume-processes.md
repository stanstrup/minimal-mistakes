---
layout: post
title: "Linux: Pause and Resume Processes"
modified:
categories: hacks
excerpt: Pause any running linux process and resume it later
tags: [linux, process, management, pause, resume]
date: 2015-03-13T02:59:33+05:30
comments: true
---

The last few days have been pretty hectic with two major assignment deadlines. And like every wild goose hunt fuelled by caffeine, they've enriched my repertoire.<br/><br/>
The **R Tree** assignment for *CS618: Searching and Indexing in Databases* involved the insertion of a million data points which took about **forty minutes** to run to completion. The program was midway through when I realized that I needed some precious CPU time for my other assignment: **fitting a mixture of Gaussian** to a data-set for *CS771: Machine Learning Tools and Techniques*.<br/><br/>
I've always maintained the racial superiority of my Dell XPS 15 but I knew better than run both these programs simultaneously. With less than three hours to D-Day, I couldn't afford terminating the **R Tree** program; it was then by divine providence that I chanced upon the idea of somehow pausing the **R Tree** program. And guess what, as it turns out, Linux has just the solution.<br/><br/>
The Linux scheduler allows to pause any running program and resume it at a later time; and the way to achieve the same is dead simple. To pause a process, run the following command:

{% highlight bash %}
$ kill -STOP <pid>
{% endhighlight %}

And at any later stage, one can resume the stopped program by issuing the following command:

{% highlight bash %}
$ kill -CONT <pid>
{% endhighlight %}

And with that I was able to pause the **R Tree** program and save the universe from destruction (Not really, but I did manage to save my grades from destruction)<br/><br/>
