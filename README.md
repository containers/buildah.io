# Container Tools

Welcome to the site for [Buildah](https://github.com/projectatomic/buildah/blob/master/README.md). This site features announcements and news around Buildah, and occasionally other [container tooling](https://github.com/containers/) news.

<ul class="posts">

  {% for post in site.posts %}
    <li><p><span>{{ post.date | date_to_string }}</span> » <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></p>
      <p>{{ post.excerpt }}</p></li>
  {% endfor %}
</ul>
