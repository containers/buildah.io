---
title: Buildah Introduction Demo
layout: default
author: tsweeney
categories: [blogs]
tags: containers, images, docker, buildah, podman, oci
---
![buildah logo](https://buildah.io/images/buildah.png)

{% assign author = site.authors[page.author] %}
# Buildah Introduction Demo 
## By {{ author.display_name }} [GitHub](https://github.com/{{ author.github }}) [Twitter](https://twitter.com/{{ author.twitter }})

I'm a pretty poor fisherman, so it's good that the old saying: "Give a person a fish and feed them for the day; teach them to fish and they're fed for a lifetime" isn't the only way I can get food.  Otherwise I'd be a shell of myself.  However a poor fisherman I am, I've found that in the tech world a demo helps me to quickly ramp up on a new technology.  

Dan Walsh ([@rhatdan](https://github.com/rhatdan)) was readying to run a Fedora Classroom doing an intro to Buildah a little while ago.  To help with that, I created a little demo script that would do a variety of calls to Buildah and would build a few container images and containers.  The images and containers in the demo are created both from "scratch" and by using a Dockerfile.  Dan added to the script showing how Buildah could be run both as root and as a non-root user.  The script and the files that the demo requires have been added to a new [containers/Demos](https://github.com/containers/Demos) project on [GitHub](https://github.com) in particular this demo is located in the [building/buildah_intro](https://github.com/containers/Demos/tree/main/building/buildah_intro)  We've made the script so that it can easily be dropped into place and then run.

Before running the script, you need to do just a little bit of prep work.  The latest Buildah (v1.6), Podman (v1.0) and Docker (1.13+) need to be installed on your system and you need to clone the containers/Demos project or copy the files from the buildah_intro directory onto it.  Then log into your system as a non-root user with sudo privileges and run the demo with ./buildah_intro.sh.

The demo will display a little note before each command in a blue color and then the Buildah command that's about to be executed in bold followed by the output of the command.  Once kicked off, you can just hit return at your own pace to see the script in action.

There are a number of other demos for Buildah and Podman in the containers/Demos project from Dan, Sally O'Malley ([@sallyom](https://github.com/sallyom)) and others.  The plan is to continue growing this new project and we're all very happy to accept any input on the current demonstrations or new demonstrations that you think are pertinent.

Hopefully you'll find this new Buildah intro script to be helpful in your learning of Buildah, at least more helpful than the fishing lessons I had!
