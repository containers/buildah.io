---
layout: default
title: Buildah
---
# {{ page.title }}

Welcome to the site for [Buildah](https://github.com/containers/buildah/blob/master/README.md). This site features announcements and news around Buildah, and occasionally other [container tooling](https://github.com/containers/) news.

![Buildah logo](images/buildah.png)

## What's New!

<section class="posts">
  {% for post in site.categories.new %}
    <p><span>{{ post.date | date_to_string }}</span> » <a href="{{ site.baseurl }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></p>
    <p>{{ post.excerpt }}</p><hr>
  {% endfor %}
</section>

#### Now where is that Container Commandos [Coloring Book](https://github.com/mairin/coloringbook-container-commandos/blob/master/Web.pdf)?
