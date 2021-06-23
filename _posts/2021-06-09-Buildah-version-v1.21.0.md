---
title: Buildah version 1.21.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.21.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.21.0](https://github.com/containers/buildah/releases/tag/v1.21.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 32, 33 & 34, and RHEL 8.5.  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon.  In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable enhancements: 

  * A `--secret` option has been added to the `bud` command, which allows passing secret information (such as a database password) to the Container without it being stored in the final image.  See the `buildah bud` man page for more information.
  *  The `buildah manifest rm` command has been added and allows the user to remove one or more manifest lists.  See the `buildah manifest` and `buildah manifest rm` man pages for more information.
  * The code that did container image handling has been removed from Buildah and replaced with the new `libimage` package that resides in [containers/common](https://github.com/containers/common/tree/master/libimage).  This code is used by a number of projects in the Containers organization and has proven to be more efficient than the older code. 

<!--readmore -->

This release comprises changes made for v1.20.0 through v1.21.0.

## Release Changes

### Changes for v1.21.0
  * Containerfiles no longer fail during CPP processing if a comment is contained within the file.
  * The `--default-mounts-file` option for the `buildah bud` command now works correctly.
  * The logrus messages for Info, Warning, and Debug are now being written to stderr when using the `buildah bud` command.
  * The check for a bad image name now happens much earlier in the build process rather than at the end.
  * When `podman build` pulled an image, it would use the `--pull-never` policy, using only the locally available image.  This has been corrected, and the image is now pulled from the registry if it is available.
  * Fixed a couple of race conditions that were causing containers to fail just before they exited.
  * The ownership of a lower directory is preserved when doing an overlay mount, similar to the way that bind mounts work.
  * The handling of images with signatures could fail under certain circumstances, this has been corrected.
  * Errors emitting from the runtime are now more clearly labeled.
  * The logic involving built-in volumes has been reworked to better handle non-overlayfs mounts.
  * Changes were made to work better with the VFS driver.
  * A `--secret` option has been added to the `bud` command, which allows passing secret information (such as a database password) to the Container without it being stored in the final image.  See the `buildah bud` man page for more information.
  *  The `buildah manifest rm` command has been added and allows the user to remove one or more manifest lists.  See the `buildah manifest` and `buildah manifest rm` man pages for more information.
  * The non functioning and unsupported `buildah bud --loglevel` option has been removed.
  * The code that did container image handling has been removed from Buildah and replaced with the new `libimage` package that resides in [containers/common](https://github.com/containers/common/tree/master/libimage).  This code is used by a number of projects in the Containers organization and has proven to be more efficient than the older code.
  * The `buildah bud` command handled multiple tags but did not report them to the user.  If there are multiple tags, `buildah bud` now reports that.  
  * Logged debugging and error messages will once again include a count of seconds elapsed since `buildah` was started.
 
### Overall Miscellaneous Changes  
* Documentation:
  * Documented the location of the auth.json file if XDG_RUNTIME_DIR is not set.
  * Updated the steps for runc users on CentOS in the install guide.
  * Removed several older distro from the install guide.
  * Minor fixes to Buildah as a library tutorial documentation.
  
* Vendored:
  * Vendor in containers/common v0.38.4
  * Vendor in containers/image/v5 to 5.12.0
  * Vendor in containers/ocicrypt to 1.1.1
  * Vendor in containers/storage to v1.31.1
  * Vendor in onsi/ginkgo to 1.16.2
  * Vendor in onsi/gomega to 1.12.0
  * Vendor in opencontainers/runc to 1.0.0-rc94
  * Vendor in openshift/imagebuilder to 1.2.2

* Tests:
  * Do not force using crun in rootless mode.
  * Fixed ‘arg missing’ warning in bud tests.
  * Check without a flag in the 'from --cgroup-parent' test.
  * Fixed a bats warning in the bud bats test.
  * The namespaces test was refactored and cleaned up.
  * Refactored the 'idmapping' system test.
  * Fixed many system tests for the 'bud' subcommand.
  * Added a system test for 'buildah help'.
  * Fixed an infinite hang in the copy.bats test.
  * Added a system test for 'buildah version`.
  * Added a few system tests for 'buildah from'. 
  * The run.bats had a flake in the run-user test that has been fixed.
  * The `:Z` option has been added to a number of tests of transient mounts.
  * Fixed an incorrect expected message when pulling an image in the bud tests.

* Changes to the build infrastructure:
  * The Buildah CI will not run the majority of its tests if the `[CI:DOCS]` tag is part of the pull requests title.
  * Notification email for cirrus-cron build failures is now sent to an email list monitored by the maintainers.
  * The GitHub action that makes the multi-arch container images on quay.io was reworked to match the actions in the Podman and Skopeo projects.
  * Cirrus: Update Fedora 34beta -> Fedora 34
  * Cirrus: Update Ubuntu image-action workflow unifications to 21.04.
  * Updated the nix pin with `make nixpkgs`.
  * Upgraded to GitHub-native Dependabot.
  * Buildah’s CI test system now requires a test to be included with a PR unless the tag `[NO TESTS NEEDED]` is included in the pull request's description.

* Plus several minor fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/main/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
