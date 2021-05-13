---
title: Buildah version 1.18.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.18.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.18.0](https://github.com/containers/buildah/releases/tag/v1.18.0) which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 32 & 33 and RHEL 8.4.  This will also be shipped on CentOS, openSUSE and Ubuntu in the near future.  In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features the notable enhancements: Short name aliases for container image names can now be declared and used more securely, the pull policy to use with the `buildah pull` command can now be specified, a few speed improvements to the build process were created, and a number of bug fixes. 

* Short name aliases can now be declared and used in a more secure manner.  For more details see this blog [post](https://www.redhat.com/sysadmin/container-image-short-names).
* The `--policy` option has been added to `buildah pull` allowing the user to specify the pull policy to use when pulling.  The valid values are: missing, always and never.  See (buildah-pull(1)](https://github.com/containers/buildah/blob/main/docs/buildah-pull.md) for details.

<!--readmore -->

This release comprises changes made for v1.17.0 through v1.18.0.

## Release Changes

### Changes for v1.18.0
  * Short-names aliasing for container images has been enhanced.
  * The `--policy` option has been added to `buildah pull` allowing the user to specify the pull policy to use when pulling.  The valid values are: missing, always and never.  See (buildah-pull(1)](https://github.com/containers/buildah/blob/main/docs/buildah-pull.md) for details.
  * A number of error messages have been changed to be more comprehensible.
  * The `--hostname` option for the `buildah run` command should work as expected for unprivileged users.
  * The `--cmd` option for the `buildah config` command should now handle an array of commands as originally designed.
  * Fixed a NPE when the path to a Dockerfile contained non-directory entries.
  * Changes were made in the way that image are built to make it more efficient. 
  * The format of the values passed to the `--userns-uid-map` and the `userns-gid-map` is now evalutated appropriately.
  * The build cache should take into account ownership differences due to ADD and COPY being used with the --chown flag.
  * Added a fix to address CVE-2019-14271.
  * Bump to v1.18.0-dev

### Overall Miscellaneous Changes  
* Documentation:
  * Update the `buildah bud` man page from the `podman build` man page.

* Vendored:
  * Vendor in github.com/containers/storage v1.24.0.
  * Vendor in github.com/containers/common v0.26.3.

* Tests:
  * Test: ensure a non-directory in a Dockerfile path is handled correctly.
  * Add a few tests for `pull` command.

* Changes to the build infrastructure:
  * Avoid overriding LDFLAGS in Makefile.
  * Update nix pin with `make nixpkgs`.
  * Use CPP, CC and flags in dep check scripts.

* Plus a number of smaller fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/main/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
