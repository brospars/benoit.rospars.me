---
layout: post
title: 'IE Fix for "jumpy" fixed background'
date: "2016-06-11 18:00:00 +0200"
author: benoit
version: 1.0.0
categories: snippets
post_description: If you are using fixed backgrounds on your website, you may experience issues on IE (I'm on IE11 Windows 8). Here's how to fix it.
---


If you are using fixed backgrounds on your website such as [here](http://impactiv.fr/), you may experience issues on IE (I'm on IE11 Windows 8).
Your fixed backgrounds may jump around and jitter when scrolling with mousewheel. (Like [this](https://www.youtube.com/watch?v=_WAaxZUvWZ8&feature=youtu.be))

A way to fix this is to disable smooth scrolling on IE, but it won't help your users.
So another way is to fix it by overriding the mousewheel event on IE like this.

{% highlight javascript %}
if(navigator.userAgent.match(/Trident\/7\./)) { // if IE
    $('body').on("mousewheel", function (event) {
        // remove default behavior
        event.preventDefault(); 

        //scroll without smoothing
        var wheelDelta = event.wheelDelta;
        var currentScrollPosition = window.pageYOffset;
        window.scrollTo(0, currentScrollPosition - wheelDelta);
    });
}           
{% endhighlight %}

Hope this can help someone :)

PS : Also -webkit-backface-visibility: hidden; can break your background-attachement in chrome (speak from experience).

-------
**This protip was originaly posted on [coderwall](https://coderwall.com/p/hlqqia/ie-fix-for-jumpy-fixed-bacground) but I start moving all my work here. So feel free to tell me what you think about it in the comment section below.**

