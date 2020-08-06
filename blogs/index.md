---
layout: default
title: Buildah Blogs
---

![Buildah logo](../images/buildah.png)

# {{ page.title }}

<section class="posts">
  {% for post in site.categories.blogs %}
    <p><h3><a href="{{ site.baseurl }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a><br><span>{{ post.date | date_to_string }}</span> by {{ post.author }}</h3></p>
  {% endfor %}
</section>
