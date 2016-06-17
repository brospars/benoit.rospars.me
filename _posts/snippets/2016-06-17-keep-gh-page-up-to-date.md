---
layout: post
title: 'Keep gh-pages up to date'
date: "2016-06-17 11:00:00 +0200"
author: benoit
version: 1.0.0
categories: snippets
comments: true
post_description: Pretty new to gh-pages ? Here's a quick tip on how to easily keep your gh-pages branch up to date with your master branch.
---

I've been using [Github Pages](https://pages.github.com/) a lot recently and it's awesome ! It provides you a quick and powerful way to host a demo of your work. But one thing that I found annoying using ``gh-pages`` is that it [suggests you](https://help.github.com/articles/creating-project-pages-manually/) to have a totally different empty branch with your demo in it and then to switch to that branch everytime you want to update your demo page, make your changes, commit to ``gh-pages`` and then push the whole thing to github. I found this a bit tedious.

But with this quick tip you can just work directly on master, make a demo page in it (aka ``index.html``), commit and push as usual and then type the followings command :

{% highlight shell %}
git checkout gh-pages
git merge master
git push origin gh-pages     
{% endhighlight %}

I'm sure it will seem obvious to a lot of you, but I'm not a git expert and before I discovered this way of doing [Github Pages](https://pages.github.com/), I was struggling keeping ``gh-pages`` branch up to date.

If you have a better way to do so, feel free to let me know.


