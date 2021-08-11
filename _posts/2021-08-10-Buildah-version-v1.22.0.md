---
title: Buildah version 1.22.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.22.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.22.0](https://github.com/containers/buildah/releases/tag/v1.22.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 32, 33 & 34, and RHEL 8.5.  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon.  In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable enhancements: 
  * To be more inclusive, the “master” branch has been renamed to “main” in the GitHub repository.  A number of changes throughout the project were made to account for this.
  * A number of changes were made to the Dockerfiles and procedures that build the Buildah container images that are on quay.io to allow them to run Buildah more easily within them, especially as a rootless user.
  * A dangling image is now considered dangling if it is “untagged”  and does not have children.  This now matches the definition used by Docker.
<!--readmore -->

This release comprises changes made for v1.21.0 through v1.22.0 and will be included in Podman v3.3.

## Release Changes

### Changes for v1.22.0
  * Changes were made to allow `dst` and `destination` to be used for targets in secret mounts.
  *  Previously, a dangling image was an “untagged” image.  This has been refined to an “untagged” image without children which emulates Docker’s definition.
  * An invalid `ADD --chown <value>` command in a Containerfile would not error [3380](https://github.com/containers/buildah/issues/3380). This has been corrected.
  * Fixed a CVE where environment values could leak into intermediate processes.
  * Reuse code from containers/common/pkg/parse.
  * `Excludes` exceptions beginning with / or ./ in a .dockerignore file were being ignored [3272}(https://github.com/containers/buildah/issues/3272) and this has been corrected.
  * No longer set 0_NONBLOCK on stdin to address [3152](https://github.com/containers/buildah/issues/3152).
  * The methods used to create a default network in a container have been moved to containers/common.
  * Added the `--env` and `--workingdir` flags to the `run` command.  See the run man page for details.
  * Added the `--json` flag to the `mount` and `version` commands.  See the mount and version man page for details.
  * The `copy` and `add` commands can now use a .containerignore file [3303](https://github.com/containers/buildah/issues/3303).
  * When copying a single file to the workdir, the workdir is no longer mistakenly overwritten [podman#10671](https://github.com/containers/podman/issues/10671).
  * The way that the auth.json file was searched for when running as a rootless user was different for a variety of commands [3259](https://github.com/containers/buildah/issues/3259).  This has been corrected to search for the file in the appropriate location.
  * Bump to v1.21.1-dev 

### Overall Miscellaneous Changes  
* Documentation:
  * Remove specific kernel version number requirement from install.md.
  * In buildah bud: --ignore-file requires a parameter.
  * In push/pull man pages: clarify supported transports.
  * Fix documentation of the --format option of buildah push.
  * Clarify `rmi` removes dangling parents in the rmi man page.
  * Fix links to containers/image master branch to the new main branch.
  
* Vendored:
  * Update nix pin with `make nixpkgs`.
  * Vendor in containers/common v0.42.1.
  * Vendor in containers/image/v55.15.0.
  * Vendor in containers/ocicrypt 1.1.2.
  * Vendor in containers/storage to 1.33.1.
  * Vendor in fsouza/go-dockerclient 1.7.3.
  * Vendor in go.etcd.io/bbolt 1.3.6.
  * Vendor in mattn/go-shellwords 1.0.12.
  * Vendor in onsi/ginkgo 1.16.4.
  * Vendor in onsi/gomega 1.14.0.
  * Vendor in opencontainers/runc 1.0.1.
  * Vendor in opencontainers/selinux 1.8.2.

* Tests:
  * The runtime-flag (debug) test now handles old and new runc.
  * Added a few tests on cgroups V2.
  * Adjust conformance-test error-message regex to account for a change in output.
  * Make it easier to override the location of the copy helper in some tests.
  * Workarounds for the appearance of differing debug messages.

* Changes to the build infrastructure:
  * Always push updated version-tagged multi-arch container images.
  * Made steps generic for the multi-arch container image build process.
  * Update cirrus-cron notification GH workflow.
  * Freshened VM images used by Cirrus.
  * Drop dependence on fedora-minimal.
  * Now Install Docker from the package cache.
  * Updates for the master->main branch rename.
  * Synchronized the workflow for multi-arch image builds across Skopeo, Buildah, and Podman.
  * Fix handling of the `--restore shadow-utils` rpm option in the container image Dockerfiles.
  * Add volumes to the container image Dockerfiles to make running Buildah within a container easier.

* Plus several minor fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
