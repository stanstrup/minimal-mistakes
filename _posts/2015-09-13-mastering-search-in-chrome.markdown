---
layout: post
title: "Mastering Custom Site Search in Chrome"
modified:
categories: tips
excerpt: "The title says it all"
tags: [tips, technical, chrome, search, custom site, google, address bar]
image:
  feature:
comments: true
date: 2015-09-13T19:36:38+05:30
---

Chrome was the shiny, fast browser which caused me to shift from firefox; and even after chrome has become the still shiny, slow mess that it has become, I find it hard to move away due to some really awesome inbuilt features of chrome. My favourite amongst them is the ability to leverage any site's search functionality. I'm pretty sure that you might have noticed that pressing `[Tab]` after typing youtube in the search bar allows you to search youtube directly from the search bar. What's really fun is that this functionality can be extended to any website as long as it searched using a URL query.<br/><br/>
For example, I'll show you how to automate searching within the settings of chrome.

- Firstly navigate to **chrome://settings** - and yes, I like to type that out.

- In the search section, you'll see a **Manage Search Engines** option.
<figure>
	<a href="/images/manage-search-engines.png"><img src="/images/manage-search-engines.png"></a>
</figure>

- Scroll to the end of the list of search engines, where it says that you can `Add a new search engine`.

- To add a new search engine, you need to name it and additionally give it a `trigger`. The trigger
   is the key which followed by a `Tab` on the omnibar lets chrome know your intent of searching the site
   instead of merely visiting it. Here I've used `csettings` as a trigger.
<figure>
  <a href="/images/example-search-engine.png"><img src="/images/example-search-engine.png"></a>
</figure>

- Fin.

