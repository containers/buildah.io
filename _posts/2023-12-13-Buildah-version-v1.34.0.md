---
title: Buildah version 1.34.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.34.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.34.0](https://github.com/containers/buildah/releases/tag/v1.34.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 38 and Fedora 39.  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon.  In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release is a quick turnaround release to shrink the size of the Buildah image via changes to the new HereDoc code.

This release comprises changes made for v1.34.0 and will be included in Podman v4.9.

## Release Changes

### Changes for v1.34.0
   * Bump to v1.33.1 by [@edsantiago](https://github.com/edsantiago) in [#5182](https://github.com/containers/buildah/pull/5182)
   * Allow using just one jail per container with `run` on FreeBSD by [@dfr](https://github.com/dfr) in [#5176](https://github.com/containers/buildah/pull/5176)

### Overall Miscellaneous Changes  
* Documentation:
   * [CI:DOCS] man pages: underscores, too-wide lines by [@edsantiago](https://github.com/edsantiago) in [#5203](https://github.com/containers/buildah/pull/5203)

* Vendored:
   * Vendor in github.com/containerd/containerd v1.7.11
   * vendor in github.com/containers/common v0.57.1-0.20231130092720-630c929caef9
   * vendor in github.com/containers/image v5.29.1-0.20231120202631-293b00ba7166
   * vendor in github.com/containers/storage v1.51.1-0.20231204015418-15c3cb7881e4
   * vendor in github.com/fsouza/go-dockerclient to v1.10.0
   * vendor in github.com/moby/buildkit to v0.12.4
   * vendor in github.com/onsi/ginkgo/v2 to v2.13.2
   * vendor in github.com/openshift/imagebuilder v1.2.6-0.20231127234745-ef2a5fe47510
   * vendor in golang.org/x/crypto to v0.16.0
   * vendor in golang.org/x/sys to v0.15.0
   * vendor in golang.org/x/term to v0.15.0

* Tests
   * Integration tests: make skip_if_no_unshare check --map-users by [@nalind](https://github.com/nalind) in [#5192](https://github.com/containers/buildah/pull/5192)

* Changes to the build infrastucture
   * Set makefile target internal/mkcw/embed/entrypoint.gz as .PHONY on non x86_64 by [@dcermak](https://github.com/dcermak) in [#5183](https://github.com/containers/buildah/pull/5183)

* Plus a few minor fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
