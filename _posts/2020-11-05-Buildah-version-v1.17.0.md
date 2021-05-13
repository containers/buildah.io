---
title: Buildah version 1.17.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.17.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.17.0](https://github.com/containers/buildah/releases/tag/v1.17.0) which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 32 & 33 and RHEL 8.4.  This will also be shipped on CentOS, openSUSE and Ubuntu in the near future.  In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah
The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features the notable enhancements:  Several new options were added to the `buildah manifest add` command, the `mount` command now returns a container name rather than a container id, changes were made to allow Buildah containers to be accessible to Podman, and a number of bug fixes. 

* The following new options have been added to the `manifest add` command: `cert-dir`, `auth-file`, `creds`, `tls-verify`.  See the [`buildah-manifest-add(1)`](https://github.com/containers/buildah/blob/main/docs/buildah-manifest-add.md) man page for details.
* The `buildah` mount command now returns a container name rather than a container id.  See the [`buildah-mount(1)`](https://github.com/containers/buildah/blob/main/docs/buildah-mount.md) man page for more details. 
* A number of internal changes were made to the Buildah containers to make them more accessible from within Podman.  Stay tuned to future announcements from Podman and Buildah.
* A number of bug fixes were made concerning the extraction of images during build processes, the setting of permissions for bind mounts, a number of bash completions were added, support for Read Only overlay mounts was corrected, and a number of other fixes. 
<!--readmore -->

This release comprises changes made for v1.16.0 through v1.17.0.

## Release Changes

### Changes for v1.17.0
  * Handle cases where other tools such as Podman mount/unmount containers.
  * Changes were made to support RO overlay mounts.
  * Changes were made use fusermount for rootless overlay umounts.
  * Fixed umount for overlay volumes.
  * Switch default log level of Buildah to Warn.
  * ADD instructions which attempt to extract archives containing PAX global extended headers should no longer trigger errors.
  * The `buildah bud` command no longer uses stdin by default.
  * Improvements were made in error reporting in cases where ADD or COPY (or "buildah add" or "buildah copy") encounter an error while attempting to create a file in a working container. 
  * The tlsVerify options now work appropriately when using insecure BUILD_REGISTRY_SOURCES in the registries.conf file.
  * Fixed an error message during a `bud` command when the Dockerfile was not in the local directory. 
  * An update fixed a regression introduced in 1.16 which caused some exceptions to exclusion rules noted in `.dockerignore` to not be copied or added from a build context. 
  * Directory ownership when copied with ID mapping is now set correctly.  Further regression tests were added to guard against this going forward.
  * The contents of archives contained in directories being copied using the ADD instruction or `buildah add` should no longer be expanded into the destination directory. 
  * Shell Completion for podman build flags were added.
  * Permissions and ownership information on the contents of archives added using the ADD instruction or "buildah add" on the command line should be preserved again. 
  * Create bind mount targets using access permission 0755 instead of 0700 for better consistency with runc.
  * Environment variables set in containers.conf will no longer be set for commands run using `buildah run` or by RUN instructions during `buildah build-using-dockerfile`.
  * A warning is now raised when setting healthcheck while configuring an image that is in OCI format.
  * The regression in `buildah add` which caused it to not properly handle source locations specified using relative paths should be fixed.
  * The `buildah mount` command now displays container names and not ids when it completes.
  * The bash completions for the  manifest options have been corrected.
  * Updates to  bash completions for the `manifest add` sub command were completed.
  * Fixes a regression where attempting to "squash" an image while committing it could fail. 
  * The following new options have been added to the `manifest add` command: `cert-dir`, `auth-file`, `creds`, `tls-verify`.  See the [`buildah-manifest-add(1)`](https://github.com/containers/buildah/blob/main/docs/buildah-manifest-add.md) man page for details. 
  * Bump to v1.17.0-dev

### Overall Miscellaneous Changes  
* Documentation:
  * Replace wget with curl in the CentOS installation instructions.
  * The `bud` flag option definitions are now sorted alphabetically in the man page.
  * Move --userns-uid-map/--userns-gid-map  description into buildah man page.
  * Added an "In Progress" section to the contributing page.
  * Conisistency issues with formatting were made across several man pages.
  * The `manifest add` man page was updated.
  * Added the  missing `--format` option in the `buildah from` man page.

* Vendored:
  * Vendor in github.com/containerd/containerd v1.4.1
  * Vendor in github.com/containers/common v0.26.2
  * Vendor in github.com/containers/image/v5 v5.6.0
  * Vendor in github.com/containers/storage v1.23.7
  * Vendor in github.com/docker/docker v17.12.0
  * Vendor in github.com/fsouza/go-dockerclient v1.6.6
  * Vendor in github.com/onsi/ginkgo v1.14.1
  * Vendor in github.com/onsi/gomega v1.10.2
  * Vendor in github.com/openshift/imagebuilder v1.1.8
  * Vendor in github.com/sirupsen/logrus from v1.7.0
  * Vendor in github.com/spf13/cobra to v1.1.1
  * Vendor in golang.org/x/sys

* Tests:
  * tests/testreport: adjust for API break in storage v1.23.6.
  * integration tests: make sure tests run in ${topdir}/tests.
  * Add a few tests of push command.
  * bud.bats: use absolute paths in newly-added tests.
  * tests: Add some tests.

* Changes to the build infrastructure:
  * CI: require that conformance tests pass.
  * CI: run gating tasks with a lot more memory.
  * New CI check: xref --help vs man pages.
  * CI: re-enable several linters.
  * CI: expand cross-compile checks.
  * Remove docs from the CI that refer to bors, since we're not using it.
  * Cirrus: Remove bors artifacts.
  * Cirrus: Skip git-validate on branches.
  * Cirrus: Fix validate commit epoch.
  * contrib/cirrus/lib.sh: don't use CN for the hostname.
  * Updates were made to the nix build processing.
  * Remove configuration for bors.
  * Lint: Use same linters as podman

* Plus a number of smaller fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/main/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
