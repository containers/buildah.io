---
layout: default
title: Buildah Release Announcements
---

![Buildah logo](../images/buildah.png)

# {{ page.title }}

<section class="posts">
  {% for post in site.categories.releases %}
    <p><span>{{ post.date | date_to_string }}</span> » <a href="{{ site.baseurl }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a> by {{ post.author }}</p>
    <p>{{ post.excerpt }}</p>
    <a href="{{ site.baseurl }}{{post.url}}"> Read More </a><hr>
  {% endfor %}
</section>
