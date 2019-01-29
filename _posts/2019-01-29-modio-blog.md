---
title: Modio uses Buildah! 
layout: default
author: tsweeney
categories: [blogs]
tags: containers, images, docker, buildah, podman, oci
---
![buildah logo](https://buildah.io/images/buildah.png)

{% assign author = site.authors[page.author] %}
# Modio uses Buildah 
## By {{ author.display_name }} [GitHub](https://github.com/{{ author.github }}) [Twitter](https://twitter.com/{{ author.twitter }})

The folks at [Modio](https://www.modio.se/index.html) are using Buildah on Fedora in GitLab-CI which allows them to have continuous integration with their CI automatically building containers.  The filesystems are built only with the necessary ingredients with the most up to date software.  Check out the full article [here](https://www.modio.se/building-container-images-with-fedora-buildah-and-gitlab-ci.html)!
