---
layout: post
title: 'Regular expression to match vtt subtitles'
date: "2018-04-17 18:00:00 +0200"
author: benoit
version: 1.0.0
categories: snippets
comments: true
post_description: This is a regular expression to match vtt and webvtt subtitles
---


**Regex** : `/^(\d{2}:\d{2}:\d{2}[.,]\d{3})\s-->\s(\d{2}:\d{2}:\d{2}[.,]\d{3})\n(.*(?:\r?\n(?!\r?\n).*)*)/gm`  
**Demo** : [https://regex101.com/r/TH1JhU/1](https://regex101.com/r/TH1JhU/1)  
**Code example** :  
```js
const regex = /^(\d{2}:\d{2}:\d{2}[.,]\d{3})\s-->\s(\d{2}:\d{2}:\d{2}[.,]\d{3})\n(.*(?:\r?\n(?!\r?\n).*)*)/gm;
const str = `WEBVTT

00:00:00.000 --> 00:00:04.469
Blah Bla bla 1
Multine
- example

00:00:04.469 --> 00:00:46.485
Blah Bla bla 2

00:00:46.485 --> 00:01:48.465
Blah Bla bla 3

00:01:48.465 --> 00:02:48.360
Blah Bla bla 4

`;
let m;

while ((m = regex.exec(str)) !== null) {
    // This is necessary to avoid infinite loops with zero-width matches
    if (m.index === regex.lastIndex) {
        regex.lastIndex++;
    }
    
    console.table(m)
}
```
