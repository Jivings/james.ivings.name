---
layout: page
title: About this Site 
header: About this site
---
{% include JB/setup %}

## Preamble

Frequently I am browsing a well executed website, having a great time, and I
wish I knew just **how it was done**.

So that my visitors will never have this problem, this page will document the
construction of this website, along with all of the technologies used. I hope
it will be of use to someone.

## Jekyll Bootstrap

The scaffolding of the site is provided by [Jekyll
Bootstrap](http://jekyllbootstrap.com). I made the decision to use JB so that I
could concentrate on content, instead of worrying about structure and management.

Also, I love Git. Using JB with Git means that all my edits are stored, and I
am able to easily push my changes to my production environment.

## Design

I have always loved web minimalism and thus always keep my eye open for new
templates. This design by Mark Reid fits the bill perfectly and just so happens
to now be one of the JB default themes.

You can read more about the thought that went into the design at [Mark Reid's
website](http://mark.reid.name/info/site.html).

## Control

The website is hosted on my VPS, which I rent from [Xilo](http://xilo.net).
This gives me a much greater level of control than standard web hosting and I
use the spare space to host my private projects.

The content of the site is written in 
[Markdown](http://daringfireball.net/projects/markdown/), using the Vim editor.
Jekyll controls the compilation of the markdown and page structure into the
static site you see before you.

The site is edited and tested locally before being pushed to my [GitHub
repository](https://github.com/Jivings/james.ivings.name) using
Git. I then checkout the new site on my VPS and the changes are automatically
published by Apache.


