---
title: Buildah version 1.11.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]
tags: community, open source, buildah
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.11.0 Release Announcement

We're pleased to announce the release of Buildah version 1.11.0 which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora, RHEL 8, RHEL 7, CentOS, openSUSE and Ubuntu in the near future.  Also container images will be available at https://quay.io/repository/buildah/stable.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  Notable enhancements:
     * Cgroups v2 is now supported. (Fedora 31 default)
     * The `--debug` option has been changed to `--log-level` for all commands.  
     * Error reporting for the `run` command has been improved.

<!--readmore-->

This release comprises changes made for v1.11.0.

## The major highlights of this release are:
 * Cgroups v2 is now supported.  This will allow cgroups to be used in rootless mode.
 * The `--debug` option has been changed to `--log-level` for all commands.  This option now takes `debug`, `info`, `warn` or `error` as an argument, defaulting to `error`.
 * The run command now reports back the error received from the container rather than ‘1’.
 * The names of images pulled from local directories are now prefixed with ‘localhost’ rather than ‘docker.io’.
 * The `buildah bud` command can now be called without arguments.
 * A number of bugs and performance improvements were created.


## Release Changes

### Changes for v1.11.0

 * The `push`, `pull` and `commit` commands now use the `$BUILD_REGISTRY_SOURCES` environment variable as documented.
 * Add a `--log-level` command line option to all commands for better log output and deprecate the `--debug` option.
 * Added support for cgroupsV2 allowing cgroups to be used in rootless mode.
 * Correctly detect ExitError values from the container when the `run` command is used.  Prior all errors were set to ‘1’ rather than the error raised by the command (Fixes https://github.com/containers/buildah/issues/1813)
 * Disabled empty logrus timestamps to reduce logger noise.
 * Updated the ‘shebangs’ in a number of shell scripts to make them more portable across different Linux distributions.
 * The names of images pulled from a local directory such as `dir:` or `oci` were always prefixed with `docker.io`, they are now instead prefixed with `localhost`.
 * Added the `--digestfile` option to the `push` commands.  When used, the manifest id of the image that was pushed is recorded in the specified file.  Also added the `Successfully pushed …` ending line as a debug statement.
 * Use digests of the added content in history entries that we create for the `ADD` and `COPY` commands.
 * Fixed a possible runtime panic in the `bud` command.
 * Add further security-related checks in the validation code of a volume.
 * When hard links were part of a copy operation, the files were sometimes copied multiple times unnecessarily, this has been corrected.
 * The performance of symlink copying operations has been improved. 
 * Allow `buildah bud` to be called without arguments.
 * A build failure has been corrected when successive `buildah bud --layers` commands were invoked and the first one used the `--target` option and the second command did not.
 * A bug has been fixed when usernamespaces were always being created in rootless mode even if they had not been configured prior to execution as they should have been.
 * Handling of /dev/null masked devices has been changed to avoid an selinux issue.
 * Bumped the upstream version  to v1.12.0-dev.

### Overall Miscellaneous Changes  
 * Documentation changes:
  * Update README.md to mention that Podman uses Buildah's API.
  * Touched up `go mod` instructions in install.md.
  * Update `bud`/`from` help to contain indicator for `--dns=none`

 * Vendored:
  * Vendor github.com/openshift/api v3.9.1-0.
  * Vendor Storage v1.13.2.

 * Tests:
  * Add --signature-policy option to several `buildah bud` tests.
  * Add bud 'without arguments' integration tests.
  * The VM images used by the Cirrus test system were updated.

 * Plus a number of smaller fixes.

## Try it Out.

If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/main/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
