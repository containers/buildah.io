---
title: Speeding up container image builds with Buildah 
layout: default
author: dwalsh 
categories: [blogs]
tags: containers, images, docker, buildah, podman, oci
---
![buildah logo](https://buildah.io/images/buildah.png)

{% assign author = site.authors[page.author] %}

# Speeding up container image builds with Buildah 
## By {{ author.display_name }} [GitHub](https://github.com/{{ author.github }}) [Twitter](https://twitter.com/{{ author.twitter }})

Dan Walsh has recently posted a blog on the [Enable Sysadmin](https://www.redhat.com/sysadmin/) site, [Speeding up container image builds with Buildah](https://www.redhat.com/sysadmin/speeding-container-buildah).  In the post, Dan walks you through how you can leverage dnf or yum to increase the speed of container builds which is especially helpful if you have many containers in your environment. 
