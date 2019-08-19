---
title: Buildah version 1.10.1 Release Announcement
layout: default
author: tsweeney
categories: [releases]
tags: community, open source, buildah
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.10.1 Release Announcement

We're pleased to announce the release of Buildah version 1.10.1 which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora, RHEL 7, RHEL 8, CentOS, openSUSE and Ubuntu in the near future.  Also container images will be available at https://quay.io/repository/buildah/stable.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  Notable enhancements.
  * A number of changes were made to `buildah config` to make removing values and volumes easier.
  * Better support for additional stores(defined in the /etc/containers/mounts.conf file).
    * Listing images now can indicate whether an image is from a read/only store
    * Deleting all images does not attempt to remove from read/only stores
    * Committing images with read/only stores now works..
  * Buildah unshare has a new `--mount` option that allows you to mount the container image while entering a user namespace.
  * Initial support for potential HPC use cases.

<!--readmore-->

This release comprises changes made for v1.9.1, v1.9.2, v1.10.0 and v1.10.1.

## The major highlights of this release are:
* If a value to the `buildah config` options `--annotation`, `--env`, `--label` or `value` has a trailing `-` (minus sign), then the value will be removed if present.
* When listing an image in json with the `buildah image` command, a ‘read only’ field has been added to the json output.
* The `buildah unshare` command has a new `mount` option.  This allows a build container to be mounted in the namespace that `buildah unshare` creates, and the path of the container’s mountpoint to be provided in an environment variable to the command that `buildah unshare` runs in that namespace.  Please reference buildah-unshare(1) for more information.
* Vendoring in Buildah is now done by ‘go mod’ instead of ‘vndr’.
* The linter used by Buildah has been upgraded to golangci-lint.

## Release Changes

### Changes for v1.10.1
  * Fixed an issue when getting credentials while using a keyring.
  * Fixed an issue with the volume ‘-’ functionality as it first didn’t check for the existence of the volume before trying to remove it.
  * Add automatic apparmor tag discovery in the Makefile when libapparmor is found.
  * The `--get-login` option on `buildah login` has been corrected to work as designed.
  * Bump version to v1.11.0-dev.

### Changes for v1.10.0
  * Added updates for `go mod` processing.
  * Configuration values can be removed by adding a `-` to the end of the value in the `buildah config` command.  This includes the `--annotation`, `--env` and the `--label` options.
  * Volumes can be removed by adding a ‘-’ to the volume name when using the `--volume` option of `buildah config` command.
  * The “Successfully pushed…” output has been removed.
  * Added the golint linter and applied fixes.
  * When deleting images, ignore read/only images.
  * Add support for listing read/only images in json output.
  * Bump version to v1.10.1-dev.

### Changes for v1.9.2
  * When importing an image, record the base image's digest, if it has one
  * Fix CNI version retrieval to not require network connection.
  * Changes were made to better handle zstd compression.
  * A `--mount` option has been added to the `unshare` command.
  * A segmentation fault has been corrected in the push command when the image name provided was nil.
  * Bump to v1.9.3-dev.

### Changelog for v1.9.1
  * The copy commands performance has been improved when a .dockerignore file is in use and it has not exclude commands.
  * On Masked path, check if /dev/null is already mounted before mounting.
  * Added a  `--mount` to `buildah run`.
  * When running rootless, the built-in slirp DNS server is added to the list of servers.
  * The `buildah run` `--volume` option now parses the input appropriately if a comma is present.
  * Converted to golangci-lint and addressed a number of issues reported by it.
  * When cleaning up at the end of a `buildah run` command, errors during the cleanup process are just logged in the debug logger.  Additional improvements to error handling in the command were also completed.
  * Bump to v1.9.2-dev.


### Overall Miscellaneous Changes  
* Documentation changes:
  * Added the overlayfs to fuse-overlayfs issue to the Troubleshooting page.
  * Added the rootless Buildah with NFS issue to the Troubleshooting page.
  * Changed `wait` to `sleep` in the buildahimage README.md page.
  * Updated the install.md page to document go mod vendoring in Buildah.

* Vendored:
  * Migrated to go mod from vndr.
  * Bump containers/image to v3.0.2.
  * Bump container/storage v1.13.1.
  * Bump github.com/containernetworking/cni to v0.7.1.
  * Bump logrus to v1.4.2.
  * Bump runc to v1.0.0-rc8.
  * Bump github.com/opencontainers/runtime-tools to v0.9.0.
  * Bump docker/libnetwork to the most recent release.

* Tests:
  * The initial implementation of the Cirrus test system was completed.
  * tests: enable overlay tests for rootless.
  * run.bats: skip the "z" flag when testing --mount.
  * Build e2e tests using the proper build tags.
  * Add bud test for RUN with a priv'd command.
  * conformance test: catch copy error.
  * chroot/run_test.go: export funcs to actually be executed.
  * tests/imgtype: ignore error when shutting down the store.
  * conformance: bud test: use raw strings for regexes.
  * conformance suite: remove unused func/var.
  * buildah test suite: remove unused vars/funcs.

* Plus a number of smaller fixes.

## Try it Out.

If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
