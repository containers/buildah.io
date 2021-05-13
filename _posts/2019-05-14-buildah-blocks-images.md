---
title: Buildah Blocks&#58; Playing with Buildah Images 
layout: default
author: tsweeney
categories: [blogs]
tags: containers, images, docker, buildah, podman, oci
---
![buildah logo](https://buildah.io/images/buildah.png)

{% assign author = site.authors[page.author] %}
# Buildah Blocks&#58; Playing with Buildah Images
## By {{ author.display_name }} [GitHub](https://github.com/{{ author.github }}) [Twitter](https://twitter.com/{{ author.twitter }})

So you always wanted to play with Buildah but you didn’t want to have to install or clone it onto your system.  Until recently you were helplessly stuck unless a good friend let you play with it on their system.  So many possible containers, so little time!

Well now if you have a containers runtime system like Podman on your machine, there are a number of container images that are now available that you can pull and then play with Buildah.  Each image has Fedora latest (version 30 at the time of this writing) and a variant of Buildah within it.
<!--readmore-->
### Buildah’s container images

The container images are available publicly on the Buildah repository on quay.io.  There are three different variants of Buildah, each in their own container image.  The first is “stable”.  The Buildah that was used to build this container image is the latest release of Buildah that’s passed through all of the production and kit testing.  Currently that’s Buildah v1.7.   

The next variant in the image is “testing”.  The version of Buildah in this image  is the version that is still in the `updates-testing` repository, but has not gone  through final testing on Fedora Updates System.  Often times this version and the stable version will be the same if  there’s no release in progress.

Finally, for those of you who hark back to the days of Evil Knievil, there’s the “upstream” variant.  Buyer beware on this one, whenever a commit is made to the Buildah project on GitHub this container image is created with the latest bits.  If you want to see how the absolute latest and greatest is working, or you want to test out the latest fix that was just merged, this is the one for you.

### Putting it Together

That’s great, but how do I use these or get to them?  Let’s take a look under the covers.  As mentioned previously, I’d recommend using Podman as the containers runtime engine.  It has the advantage of not requiring a daemon and has a CLI that is very familiar to those that have run Docker.

```
$ podman pull docker://quay.io/buildah/stable:latest
Trying to pull docker://quay.io/buildah/stable:latest...Getting image source signatures
Copying blob a3ed95caeb02 done
{A lot of happy pull information removed for brevity}
Writing manifest to image destination
Storing signatures
b1006027935c8906bf54aa323be86b23c9bae1349b5d43af1614d1240a8a7d0a

$ podman run stable buildah version
Version:         1.7
Go Version:      go1.11.5
Image Spec:      1.0.0
Runtime Spec:    1.0.0
CNI Spec:        0.4.0
libcni Version:  
Git Commit:      
Built:           Thu Jan  1 00:00:00 1970
OS/Arch:         linux/amd64

```

OK, that’s kind of neat, we’ve the stable image pulled down and we’ve created a container from it.  A quick side note, just replace the word “stable” in the pull command above with either “upstream” or “testing” if you want to use one of those variants.  Let’s just peak at the image we pulled down.

```
$ podman images
REPOSITORY                 TAG      IMAGE ID       CREATED        SIZE
quay.io/buildah/stable     latest   b1006027935c   19 hours ago   332 MB
```

### Taking Buildah for a test run

Now that the engine is warmed up, let’s take it for a little more than a test spin.  Let’s build a new container image that when run will accept a city name and will then spit out the current weather there.  First we’ll need to have two files locally, a small python script and a Dockerfile to build our new “weather” image.  Both files are available at [GitHub](https://github.com/containers/Demos/tree/main/building/myweather) and for reference the Dockerfile contains:

```
$ cat Dockerfile.weather
FROM quay.io/buildah/stable
RUN yum install -y python3 python-pip
RUN pip3 install requests
COPY weather.py /
CMD  python3 weather.py
```

Now that we’ve our two files, let build the weather image and then run it.  In the example below I put in “Boston” from the command line.

```
$ podman build -t weather -f Dockerfile.weather .
STEP 1: FROM quay.io/buildah/stable
Getting image source signatures
{A lot of happy build information removed for brevity}
STEP 5: COMMIT weather
--> 5b5058fc5c1f46eb9af658d3b4e32728e0e2523b9e83bf1836511532d2b8cce5

$ podman run --tty=true -a=stdin -a=stdout weather
Enter the city: Boston

Boston's temperature: 66.34°F | 19.08°C
Wind speed: 10.29 mph | 4.6 m/s
Description: clear sky
Weather: Clear
```

Or alternatively with Buildah using the image Podman built:
```
$ buildah from --name myweather weather
myweather

$ buildah run myweather python3 weather.py
Enter the city: Boston

Boston's temperature: 66.34°F | 19.08°C
Wind speed: 10.29 mph | 4.6 m/s
Description: clear sky
Weather: Clear
```

## Wrapping up

Using one of the prebuilt Buildah images is a great way to run a quick test of the version of Buildah that’s of most interest to you.  It might also be a good way to do a proof of concept using one of your scripted builds or to verify that the latest Buildah provides updated functionality that you need in your production environment.  The best part is it’s quick, simple and ready to go.

**Buildah == Simplicity**
