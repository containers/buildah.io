---
title: Buildah version 1.13.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]
tags: community, open source, buildah, hpc
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.13.0 Release Announcement

We're pleased to announce the release of Buildah version 1.13.0 which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora, RHEL 8, RHEL 7, CentOS, openSUSE and Ubuntu in the near future.  Also container images will be available at https://quay.io/repository/buildah/stable.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release had a quick release cadence due to a few critical issues with volume handling.  Notable enhancements:

* Changes to unmount volumes cleanly and to handle full volume specifications in the `bud` command.
* `$TMPDIR`, which defaults to `/var/tmp` is now used when pulling and pushing images.
* Further support added to enable FIPS-Mode.
<!--readmore -->

This release comprises changes made for v1.13.0.

## Release Changes

### Changes for v1.13.0
* The version of containers/storage vendored in this release has a fix to handle the situation when a volume was ‘unmounted’ by the user, but due to namespace handling, the counter tracking the number of mounts the volume had was not decremented as it should have been.
* Fixed option handling for volumes in build.  If a volume specification had a comma within it i.e. `myvol:/myvol:rw,Z`, the CLI parsed the `,Z` incorrectly and errored.
* Reworked the overlay pkg so it could be more easily shared with libpod.
* Fixed buildahimage builds for the Buildah images on quay.io.  The shadows-utils package is now installed on those images and a default user `build` has been added to force the generation of the `/etc/subuid` and `/etc/subgid` files.  This should allow for the building of a container in that image by a non-root user.
* Add support for FIPS-Mode backends to the project.
* The TMPDIR used for pushing and pulling images is now set to `$TMPDIR`.  By default this points to the `/var/tmp` directory.  This should correct the issue of running out of space when doing a push or pull.

### Overall Miscellaneous Changes  
* Vendored:
  * Bump github.com/containers/storage to v1.15.5
  * Bump github.com/containers/image/v5 from 5.0.0 to 5.1.0
  * Bump github.com/containers/common from 0.0.3 to 0.0.5

* Tests:
  * Develop a safer test for pull --all-tags
  * BATS major cleanup: blobcache.bats: refactor
  * BATS major cleanup: Added a number of missing ‘run_buildah’ commands, changed the log-level in the tests, and a number of small cleanups throughout.

* Plus a number of smaller fixes.

## Try it Out.

If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
