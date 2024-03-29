---
title: Buildah version 1.1 Release Announcement
layout: default
author: tsweeney
categories: [releases]
tags: community, open source, buildah
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.1 Release Announcement

![buildah logo](https://cdn.rawgit.com/containers/buildah/main/logos/buildah-logo_large.png)

We're pleased to announce the release of Buildah version 1.1 which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora, RHEL 7, CentOS and Ubuntu in the near future.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix, launching new functionality and creating a number of improvements and bug fixes.  

<!--readmore-->

## The major highlights for this release are:

 * Drop capabilities if running container processes as non root
 * Print Warning message if cmd will not be used based on entrypoint
 * Add OnBuild support for Dockerfiles
 * Add support for buildah bud --label
 * Report errors on bad transports specification when pushing images
 * Add registry errors for pull
 * Give better messages to users when image can not be found
 * Add environment variable to buildah --format
 * Accept json array input for config entrypoint
 * buildah bud now requires a context directory or URL
 * buildah bud picks up ENV from base image
 * Run: set supplemental group IDs
 * Use CNI to configure container networks
 * add/secrets/commit: Use mappings when setting permissions on added content
 * Add CLI options for specifying namespace and cgroup setup
 * Always set mappings when using user namespaces
 * Read UID/GID mapping information from containers and images
 * build-using-dockerfile: add --annotation
 * Implement --squash for build-using-dockerfile and commit
 * Manage "Run" containers more closely
 * Handle /etc/hosts and /etc/resolv.conf properly in container
 * Make "run --terminal" and "run -t" aliases for "run --tty"
 * buildah push/from can push and pull images with no reference
 * Attempt to download file from url, if fails assume Dockerfile
 * builder-inspect: fix format option
 * buildah-from: add effective value to mount propagation
 * Documentation Changes
 * Change freenode chan to buildah
 * Add example CNI configurations
 * Touch Up tutorial for run changes
 * Update 01-intro.md tutorial
 * Update troubleshooting with new run workaround
 * Add console syntax highlighting to troubleshooting page
 * Touchup man page short options across man pages
 * Demo Changes
   * Added demo dir and a demo.
   * Added Docker compatibility demo
   * Added a bud demo and tidied up
   * Update buildah scratch demo to support el7
   * Quick fix on demo readme
 * Test Changes
   * Add tests for namespace control flags
   * CI tests and minor fix for cache related noop flags
   * Add cpu-shares short flag (-c) and cpu-shares CI tests
   * Add buildah bud CI tests for ENV variables
   * Additional bud CI tests
   * Run integration tests under travis_wait in Travis
   * Re-enable rpm .spec version check and new commit test
   * Update to F28 and new run format in baseline test
   * Add context dir to bud command in baseline test
   * add test to inspect
   * Test with Go 1.10, too
   * rmi, rm: add test
   * add mount test
   * Fix SELinux test errors when SELinux is enabled
 * Vendor changes
   * Vendor in latest container/storage for devicemapper support
   * Vendor github.com/onsi/ginkgo and github.com/onsi/gomega
   * Vendor github.com/containernetworking/cni v0.6.0
   * Update github.com/containers/storage
   * Update github.com/containers/libpod
   * Vendor in latest containers/image
 * Plus a number of smaller fixes.

## Try it Out.

If you haven’t yet, install Buildah from the Fedora repo or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us in GitHub, where Open Source communities live.

## Buildah == Simplicity
