---
title: Buildah version 1.6 Release Announcement
layout: default
author: tsweeney
categories: [releases]
tags: community, open source, buildah
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.6 Release Announcement

We're pleased to announce the release of Buildah version 1.6 which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora, RHEL 7, CentOS, openSUSE and Ubuntu in the near future.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  Updates were made to the performance of many commands, a `buildah info` command has been added, Dockerfile processing updates and bug fixes.

<!--readmore-->
## The major highlights for this release are:

* Many performance changes have been made throughout the image handling code including but not limited to faster compression and parallel pulls of images.  Note: the output of the `buildah pull` command has changed slightly to reflect these changes.

* The `buildah info` command was added to display relevant system information.

* A number of changes were made in the way that Dockerfiles are processed including processing one-line Dockerfiles, processing the `COPY --from` command, processing the `ADD --chown` command and several performance related changes.

## Release Changes

* The unshare command no longer overrides the USER environment variable.
* The `--chown` parameter when used with the ADD command in a Dockerfile is now supported.
* The run command no longer double logs the last output from some processes.
* The no_pivot_root option now works with the run command when running rootless.
* A CreatedAtRaw date field is usable with the `buildah images` command using the format option.
* The json output from the `buildah images` command was not properly formatted and this has been corrected.
* Added an all-tags option to the pull command.  When specified every tag will be pulled for the image, not just ‘:latest’.
* Fix support for multiple short options.  I.e. `buildah run -t -v {container} {command}` can now be specified as `buildah run -tv {container}{command}`.
* Remove duplicate entries from `buildah images` JSON output.
* A superfluous warning about the ‘Hostname’ being set in an image has been removed unless the user is overriding the hostname via the command line.
* Add aliases for `buildah containers` so `buildah list`, `buildah ls` and `buildah ps` work.
* The pgzip package has replaced the compress/gzip package which improves both pull and push performance.
* Changes have been made to the mount functionality when in rootless mode and not using the ‘vfs’ driver.  Reference bulidah-mount(1) for more information.
* The `buildah images -q` command has been fixed.
* A `--platform` noop option has been added to the `buildah bud` command for interoperability with other container technologies.  Buildah currently supports only Linux.
* Makefile changes:
  - Cleaned up number of variables
  - Packagers can now more easily add tags
  - The requirement on git has been softened
* When a /etc/passwd file was not in the container, `buildah run` would fail to run.  Now Buildah assumes it should run as root instead. 
* Added the `buildah info` command.
* Enable --quiet when the --filter option is also used with the `buildah images` command.
* The `--filter dangling=true` option now works for `buildah images` as documented.
* Changes related to Dockerfile handling:
  - One-line Dockerfiles are now processed appropriately.
  - When building using a Dockerfile, the commit process disables compression by default.
  - The 'ADD --chown' command in a Dockerfile is now handled appropriately.
  - The 'COPY --from' command in a Dockerfile is now handled appropriately.
  - The containers hostname wasn’t always set properly when using RUN inside of a Dockerfile, this has been corrected.
  - Added the `--disable-compression` option to the ` buildah build-using-dockerfile` command.
* Documentation changes:
  - Information posted on how to mount in rootless mode.
  - Clarification on docker.io being the default for the `buildah push` command when pushing to docker-daemon.
  - A variety of small clarifications and touch ups.
* Tests: A number of corrections and creations were added.
* Plus a number of smaller fixes.

## Try it Out.

If you haven’t yet, install Buildah from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
