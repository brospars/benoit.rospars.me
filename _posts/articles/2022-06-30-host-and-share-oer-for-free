---
layout: post
title: 'A way to host and share Open Educational Resources for free'
date: "2022-06-30 18:00:00 +0200"
author: benoit
version: 1.0.0
categories: articles
comments: true
post_description: In this article I will share a way to host, present and share open educational resources without for free using common tools and practice from the developers community
---

## The context

We, at Inria, provide free and open courses about computer science on the
french national mooc platform : France Université Numérique ([FUN](https://fun-mooc.fr)).

It's great and we reached a large audience using fun-mooc. But it has 3 major
drawbacks :

- Contents can only be accessed by signup users
- Moocs are limited in time (session 3 months to 1 year)
- The content on the LMS is not open to contribution (only the pedagogical team can edit it)

So the content is not easily sharable and, after some time, become deprecated or unreachable.

### A better workflow

As a developer, I hate to go on the WebUI to type some text on a wysiwyg editor
and our authors (computer scientists) hate it too. So, our team had to go back
and forth with our authors over emails or cloud documents to copy/upload the
document on the LMS throughout the project.

We decided to use Github/Gitlab and markdown to have a lightweight syntax for
writing course content and hosting images and documents.

It was so obvious to me that this is the best to tool to host and share contents
with anyone and open it to contributions. But it was not so obvious in the e-learning
community since we also have non-technical authors and pedagogical team members.

So, this solves 2 problems :
- Always accessible
- Open to contributions

But Github/Gitlab can be repellent for non-technical users and intimidating to
browse a repository. So we wanted a more user-friendly website to be accessible by anyone.

### A public website

Since we have all the content in markdown with images and embed of Youtube videos.
We are one step away to publish it as a static website on Github/Gitlab pages.
We choose [Mkdocs Material](https://squidfunk.github.io/mkdocs-material/) in our
case but it could be any markdown documentation generator. This provide a nice
static and customisable website with a powerful search engine. You can see an
example in our [Environmental impacts of digital technologies](https://learninglab.gitlabpages.inria.fr/mooc-impacts-num/mooc-impacts-num-ressources/en/index.html)
course.

![Environmental impacts of digital technologies](/img/impact-num-course.png)

We also use [Jupyter books](https://jupyterbook.org/en/stable/intro.html) for courses
that uses Jupyter Notebooks as the main course support, such as our
[Scikit-Learn](https://inria.github.io/scikit-learn-mooc/) course.


![Scikit-Learn](/img/scikit-learn-course.png)

### Integrate it in the LMS

Once we have our static website ade, we want to integrate its content to not multiply the sources of information. Thus we fetch the html content and insert it in a html component of the LMS using Javascript.

To fetch HTML from another website using JavaScript, we can use the fetch API. The fetch API allows us to make HTTP requests to other URLs and retrieve their content. Here is an example of how we can use the fetch API to fetch HTML from another website:

```html
<div id="external-content"></div>
```

```js
fetch('https://something.github.io/awesome-content')
.then(response => response.text())
.then(html => {
    document.querySelector('#external-content').innerHTML = html
});
```

In this example, the fetch method is called with the URL of the website hosted on Github/Gitlab pages that we want to fetch the HTML from. The then method is used to handle the response from the fetch call. The response.text() method is used to convert the response to a string of plain text, which is then passed as the html argument to the next then callback.

In the second then callback, we insert the HTML into the current LMS page using the innerHTML property of an HTML element.

**Note:** The fetch API is not supported in all browsers, so you may need to use a polyfill or a different HTTP library to support older browsers. Consult the documentation for the fetch API or your chosen HTTP library for more information on how to do this.

We can go a step further and make a utility class to fetch and insert html for every html node that contains a certain `class` and `data-url` :

```js
document.querySelectorAll('.external-content').forEach(function(el) {
  if (!el.dataset.url) return;
  insertContent(el, el.dataset.url)
})

function insertContent(el, url) {
  fetch(url)
  .then(response => response.text())
  .then(html => {
    el.innerHTML = html
  });
}
```

Then we simply use our class to insert multiple content from different pages :

```html
<div class="external-content" data-url="https://something.github.io/awesome-content-1"></div>

<div class="external-content" data-url="https://something.github.io/awesome-content-2"></div>

<div class="external-content" data-url="https://something.github.io/awesome-content-3"></div>
```


### Conclusion

Good workflow and centralizing the sources of information may seems obvious for us developer but might not
be so obvious for people with less technical backgrounds. We need to share to non-technical peoples
our tools and good practices to show that dev tools can be used in other contexts as well.
