---
title: Buildah version 1.26.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.26.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.26.0](https://github.com/containers/buildah/releases/tag/v1.26.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 35 and Fedora 36.  Buildah will also be shipped on CentOS, OpenSUSE, RHEL, and Ubuntu soon.  In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable enhancements: 
<!--readmore -->
   * The `buildah build` command now includes a `--env` option to complement its `--unsetenv` option.
   * The `buildah build` and `buildah config` commands now accept `--os-version` and `--os-feature` flags for setting the corresponding fields in an image's configuration.
   * Custom build outputs are now allowed ([#3789](https://github.com/containers/buildah/issues/3789)) and the type and destination can be selected.  

This release comprises changes made for v1.25.1 and the main branch and will be included in Podman v4.1.1.

## Release Changes

### Changes for v1.26.0
   * Changes were made to the copy algorithm of the build command to prevent concurrent read/write actions on the internal maps.
   * The `buildah build` command now includes a `--env` option to complement its `--unsetenv` option.  See the [buildah-build.1.md](https://github.com/containers/buildah/blob/main/docs/buildah-build.1.md) man page for details.
   * The default value of the `io.buildah.version` label can now be overridden at the `buildah build` command line using the `--label` option.  See the [buildah-build.1.md](https://github.com/containers/buildah/blob/main/docs/buildah-build.1.md) man page for details.
   * The `buildah build` and `buildah config` commands now accept `--os-version` and `--os-feature` flags for setting the corresponding fields in an image's configuration.  See the [buildah-build.1.md](https://github.com/containers/buildah/blob/main/docs/buildah-build.1.md) and [buildah-config.1.md](https://github.com/containers/buildah/blob/main/docs/buildah-config.1.md) mang pages for details.
   * The `TARGETPLATFORM` variable in the build process is now set correctly when one or more `--platform` options are specified.
   * When the `--layers` option was used, `build` did not always handle aliases as it should ([#3939](https://github.com/containers/buildah/issues/3939)).  This has been corrected.
   * Custom build outputs are now allowed ([#3789](https://github.com/containers/buildah/issues/3789)) and the type and destination can be selected.  See the `--output` option on the [buildah-build.1.md](https://github.com/containers/buildah/blob/main/docs/buildah-build.1.md) man page for more information.
   * An error that at times did not allow for a file to be written to a directory during the build process has been corrected.
   * Error messages now use consistent lowercase 'invalid' in returned error messages.
   * The hostname within the container is now set to the server’s hostname rather than “localhost”.
   * Fixed an error where only an image with a shortname could be pushed ([3915](https://github.com/containers/buildah/issues/3915)).
   * The network backend is now initialized appropriately before the first pull rather than defaulting to cni more times than it should have.
   * Changes were made to the mount functionality called when in a rootless environment to mount volumes appropriately.
   * Buildah now uses the settings in containers.conf for ‘netns’ configuration.
   * The `buildah build` command only accepts at most one argument, it errors now when multiple arguments are given instead of ignoring them.
   * When trying to add a local image to the manifest while also setting the variant or arch, would fail to find the local image and would pull it from the registry ([#3511](https://github.com/containers/buildah/issues/3511)).  This has been corrected.
   * The `io.buildah.version` labels can now be suppressed ([#3826](https://github.com/containers/buildah/issues/3826)) in the `build` and `commit` commands with the `--identity-label` option.  See the [buildah-build.1.md](https://github.com/containers/buildah/blob/main/docs/buildah-build.1.md) and [buildah-commit.1.md](https://github.com/containers/buildah/blob/main/docs/buildah-commit.1.md) man pages for details.
   * Containers created by running "buildah from" and specifying the base image using its full ID, or during a "buildah build", will be given shorter auto-generated names.
   * Fixed a hang caused by a timing issue when the oci runtime would fail.
   * Fixed an error when running in rootless, not all processes were killed that should have been.
   * Bump back to v1.26.0-dev

### Overall Miscellaneous Changes  
* Documentation:
   * The option usage text across the manpages was made more consistent.
   * The FreeBSD builds for documentation have been fixed.

* Vendored:
   * Vendor in github.com/containerd/containerd 1.6.15
   * Vendor in github.com/containerd/containerd 1.6.4
   * Vendor in github.com/containernetworking/cni 1.1.0
   * Vendor in github.com/containers/common 0.48.0
   * Vendor in github.com/containers/image 5.21.1
   * Vendor in github.com/containers/storage 1.40.2
   * Vendor in github.com/fsouza/go-dockerclient 1.7.11
   * Vendor in github.com/opencontainers/runc 1.1.1
   * Vendor in github.com/opencontainers/selinux 1.10.1
   * Vendor in github.com/openshift/imagebuilder 1.2.4

* Tests:
   * Tests were added for the `--platform` option with the Containerfile’s `FROM` command and also for builtinargs behavior.
   * Renamed the variable `$TESTSDIR` (the plural one), to `$TESTDIR` within the tests.
   * Issues with some corner cases involving assert calls were corrected.
   * Concurrency was reduced in the flaky `bud-multiple-platform-no-run` test.
   * Rootless on cgroupv2 in the root environment is now skipped.
   * The copier tests now use the correct UID/GID in test archives.
   * Some of the integration tests now use a dummy registry.

* Changes to the build infrastructure:
   * The build now automatically sets the correct `TARGETPLATFORM` where expected.
   * Updated the  CI VMs to Fedora 36.
   * Fixed a static check linter warning for a deprecated function.
   * Set permissions correctly for a few GitHub actions.

* Plus several minor fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
