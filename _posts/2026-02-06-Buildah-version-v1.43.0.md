---
title: Buildah version 1.43.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.43.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.43.0](https://github.com/containers/buildah/releases/tag/v1.43.0), which is now available from GitHub for any Linux distro. We are shipping this release on Fedora 42 and Fedora 43. Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon. In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix. This release features one notable change: 
<!--readmore -->
 * Fixes for several runc CVEs and follow-on regressions.

This release comprises changes made for v1.43.0 and will be included in Podman v5.8.

## Release Changes
### Changes for v1.43.0
  * [release-1.42] Bump runc to v1.3.4 to fix CVE-2025-31133, CVE-2025-52565, and CVE-2025-52881 and regression fixes to runc by [@TomSweeneyRedHat](https://github.com/TomSweeneyRedHat) in [#6560](https://github.com/containers/buildah/pull/6560)
  * [release-1.42] Run: don't try to encode SystemContext with json by [@nalind](https://github.com/nalind) in [#6565](https://github.com/containers/buildah/pull/6565)
  * [release-1.42] chroot.bats(chroot with overlay root): ensure we can overlay by [@nalind](https://github.com/nalind) in [#6566](https://github.com/containers/buildah/pull/6566) 

* Vendored: 
  * Vendor in github.com/opencontainers/runc v1.3.4
 
* Tests
* [release-1.42] tests: use cached images instead of fedoraproject.org by [@nalind](https://github.com/nalind) in [#6667](https://github.com/containers/buildah/pull/6667)
  * [release-1.42] test: do not untar archive into fs when checking file names by [@nalind](https://github.com/nalind) in [#6668](https://github.com/containers/buildah/pull/6668)

* Changes to the build infrastructure
   * [release-1.42] fix(build): make --tag oci-archive:xxx.tar work with simple images by [@nalind](https://github.com/nalind) in [#6669](https://github.com/containers/buildah/pull/6669) #6669

### **Full Changelog**: https://github.com/containers/buildah/compare/v1.42.2...v1.43.0

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin. We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions! If you haven't joined our community yet, don't wait any longer! Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity

