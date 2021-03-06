---
title: Lightweight CSS Grid Framework
desc: CSS Grid is being supported by most of the browsers. I have created a framework built around this for my next websites. The CSS weighs only around a Kilobyte! I hope other frameworks migrate to CSS Grid soon. 
author: sharathdt
tags: Web-Design Opinion
image: css-grid-framework.png
img-src: ""
img-src-name: Design by Freepik
layout: post
permalink: /css-grid-framework/
sec: 
---

I have been using [Bootstrap](http://getbootstrap.com/){: target="_blank"}{: rel="nofollow"} to design most of my client websites. For simpler ones I have used [Skeleton](http://getskeleton.com){: target="_blank"}{: rel="nofollow"}. These frameworks are great but most of the times I use these frameworks for just one purpose - the rows and columns. 

Now, my problem with them is that they are heavy. It is so because bootstrap has style defined for almost all kinds of html elements. Many times we don't even use half of those styles. Also, for grid layout(rows and columns) they use either float or flexbox. If something is floated then it is necessary to clear it. This increases the code size a little bit.

Also, floated elements come out of the parent element wrapper and it looks weird. You will have to use clearfix to clear the float.

![Float Problems](/images/float-problems.svg)

{% include treehouse-1.html %}

## CSS Grids

CSS Grids has been around for a long time but is not being used as much. I was astonished by its simplicity and wondered why no one ever used it in any of the frameworks. Is there one? let me know.

![Float Problems](/images/css-grid-framework.svg){: target="_blank"}


There are no floats and flex directions. Also, a new unit called fraction which can replace percentages.

Read: [How to speed up Jekyll website](/jekyll-speed/)

## Usage

Here is a simple pen from Rachel Andrew showing how easy it is to create grids using CSS Grids.

<p data-height="300" data-theme-id="light" data-slug-hash="BNXyQa" data-default-tab="css,result" data-user="rachelandrew" data-embed-version="2" data-pen-title="Grid by Example 1: Defining a Grid" class="codepen">See the Pen <a rel="nofollow" href="https://codepen.io/rachelandrew/pen/BNXyQa/">Grid by Example 1: Defining a Grid</a> by rachelandrew (<a rel="nofollow" href="https://codepen.io/rachelandrew">@rachelandrew</a>) on <a rel="nofollow" href="https://codepen.io">CodePen</a>.</p>


## Framework

I thought of creating a framework around CSS Grids for easy prototyping. I have designed the demo website using the same Framework. 

The CSS used for Grid layout is smaller than a Kilobyte! That should make a site superfast. Here is the website - [**Web Grid**](http://webjeda.com/web-grid/){: target="_blank"}

This is an open source project. Make use of this in your next project. Also, contribute by improving it, if you would like to.


There is one major issue - [browser support](http://caniuse.com/css-grid/embed){: target="_blank"}{: rel="nofollow"}. Almost all the browsers do support CSS Grids except for few mobile browsers like UC and Opera mini. I hope they will adopt this pretty soon.


## Reference Links

[MDN CSS Grids](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout){: target="_blank"}

[Grid by Example](https://gridbyexample.com/examples/){: target="_blank"}



<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>