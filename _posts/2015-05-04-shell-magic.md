---
layout: post
title: "Shell Magic"
modified:
categories: technical
excerpt: "Saving an Ubuntu in distress with some commandline-fu"
tags: [linux, sed, awk, grep, apt-get, technical]
image:
  feature:
date: Mon May  4 15:45:32 IST 2015
comments: true
---

The other day, a friend of mine ran the following command in an attempt to remove wine and it's dependants.

{% highlight bash %}
$ sudo apt-get purge wine *
{% endhighlight %}

Unfortunately for him, the command worked and did end up removing wine with a whole lot of other system critical
packages. In an attempt to resuscitate his computer, he tried rebooting it and in the moments that ensued, I can
swear I saw the living daylights sucked out of his face. But every cloud has a silver lining and despite the fact
that we could not boot into X, we did have shell access. <br><br>
Fortunately for us, **apt** maintains a log of all the operations it performs in */var/log/apt/term.log* and while
it would have been easy to just manually make a list of programs that were uninstalled, it wasn't [half-assed
](https://www.youtube.com/watch?v=sCZJblyT_XM) enough. Instead, we summoned the Gods of the shell to aid us in
this conquest.<br><br>
We began by getting the relevant portion of the log file to another file (while it is possible to work with the
same log file, we didn't want to go through the hassle of using **sudo** every time we had to access the log file.)

{% highlight bash %}
$ sudo tail -177 /var/log/apt/term.log > temp.log
{% endhighlight %}

I'll admit, we cheated a bit by using **177** and while it could have been programmed easily using **grep**, we were
more excited about what we had to do next to really worry about making all of this reproducible.

{% highlight bash %}
Log started: 2015-05-01  10:36:15
Removing cmake
Processing triggers for man-db
Log ended: 2015-05-01  10:36:29
{% endhighlight %}

As you can see above, **apt** logs all removed programs as *Removing <program_name>*, so a simple **grep** search
would list all the lines containing the removed programs and the second field of these lines would get us
a list of all the programs which were removed by this operation. <br>

{% highlight bash %}
$ cat temp.log | grep '^Removing' | awk '{print \$2}'
{% endhighlight %}

The carat in **grep**'s argument signifies that we want all lines starting with the word 'Removing'. Also,
we use **awk** to obtain the second field of the lines (an astute reader may suggest alternatives like
**cut** as well). <br><br>
Now that we had a list of the uninstalled programs, all that is left is feeding this list to **apt** for
installation.

{% highlight bash %}
$ cat temp.log | grep '^Removing' | awk '{print \$2}' | xargs sudo apt-get install -y
{% endhighlight %}

And viola! All was back to normal in Linux Land.
