---
title: Buildah version 1.40.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.40.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.40.0](https://github.com/containers/buildah/releases/tag/v1.40.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 41 and Fedora 42.  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon. In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable changes: 
<!--readmore -->
 * The `--inherit-labels` option has been added to inherit labels from the base image, or not.
 * Add a `--parents` option for the `COPY` command to preserve leading directories in the paths of items being copied, relative to either the top of the build context, or to the "pivot point".
 * The `--timestamp option`, if set, is now passed through to a destination of `--tag=oci-archive` and is applied to the timestamp of entries in the tar archive

This release comprises changes made for v1.40.0 and will be included in Podman v5.5.

## Release Changes
### Changes for v1.40.0
   * Bump Buildah to v1.39.0, c/storage v1.57.1, c/image v5.34.0, c/common v0.62.0 by [@TomSweeneyRedHat](https://github.com/TomSweeneyRedHat) in [#5962](https://github.com/containers/buildah/pull/5962)
    *The host directory used when a `buildah build` RUN instruction or `buildah run` uses the `--mount=type=cache` option is now chosen based not only on its "target" or "id" value, but also on the combination of "uid" and "gid" flag values specified, by [@nalind](https://github.com/nalind) in [#5978](https://github.com/containers/buildah/pull/5978)
   * Better support for the containers.conf container_name_as_hostname option by [@nalind](https://github.com/nalind) in [#5943](https://github.com/containers/buildah/pull/5943)
   * Better validation of manifest and expected digests by [@mtrmac](https://github.com/mtrmac) in [#6014](https://github.com/containers/buildah/pull/6014)
   * stage_executor: history now correctly includes the heredoc summary by [@flouthoc](https://github.com/flouthoc) in [#6041](https://github.com/containers/buildah/pull/6041)
   * Add `--parents` option for the `COPY` command to preserve leading directories in the paths of items being copied, relative to either the top of the build context, or to the "pivot point" by [@Honny1](https://github.com/Honny1) in [#6008](https://github.com/containers/buildah/pull/6008)
   * The  /proc/interrupts and /sys/devices/system/cpu/*/thermal_throttle are thermal paths are masked by default by [@giuseppe](https://github.com/giuseppe) in [#6074](https://github.com/containers/buildah/pull/6074)
   * Fix built-in args on ARM64 by [@Honny1](https://github.com/Honny1) in [#6076](https://github.com/containers/buildah/pull/6076)
   * The --timestamp option, if set, is now passed through to a destination of --tag=oci-archive: and is applied to the timestamp of entries in the tar archive by [@aeijdenberg](https://github.com/aeijdenberg) in [#6023](https://github.com/containers/buildah/pull/6023)
   * "chroot" isolation should no longer require the "--no-pivot" flag be specified in order to function on "image mode" systems. by [@nalind](https://github.com/nalind) in [#6088](https://github.com/containers/buildah/pull/6088)
   *  Fixed a bug to add: correctly resolve git tags and branches and report errors if no reference is found by [@flouthoc](https://github.com/flouthoc) in [#6087](https://github.com/containers/buildah/pull/6087)
   * Fixed a bug in processing Windows style paths by [@danegsta](https://github.com/danegsta) in [#6083](https://github.com/containers/buildah/pull/6083)
   * Return status 125 when a git operation fails instead of relaying the error code directly from git by [@flouthoc](https://github.com/flouthoc) in [#6092](https://github.com/containers/buildah/pull/6092)
   * The build process now resets the platform in systemcontext for every stage by [@flouthoc](https://github.com/flouthoc) in [#5971](https://github.com/containers/buildah/pull/5971)
   * Allow users to choose if they want to inherit labels from the base image by using --inherit-labels option  by [@flouthoc](https://github.com/flouthoc) in [#6103](https://github.com/containers/buildah/pull/6103)
   * Certain errors encountered when calling `mount()` while using "chroot" isolation will now use mount flag names in error diagnostic messages by [@nalind](https://github.com/nalind) in [#6129](https://github.com/containers/buildah/pull/6129)
   * A bug was fixed to close files after a build properly by [@aeijdenberg](https://github.com/aeijdenberg) in [#6047](https://github.com/containers/buildah/pull/6047)
      
### Overall Miscellaneous Changes  
* Documentation:
   * Switch to the CNCF Code of Conduct by [@mheon](https://github.com/mheon) in [#5982](https://github.com/containers/buildah/pull/5982)
   * buildah-build.1.md: secret examples by [@hdub-tech](https://github.com/hdub-tech) in [#5999](https://github.com/containers/buildah/pull/5999)
   * Add a link to project governance and MAINTAINERS file by [@mheon](https://github.com/mheon) in [#6108](https://github.com/containers/buildah/pull/6108)
   * [CI:DOCS] Document rw/src for --mount in buildah-run(1) by [@nalind](https://github.com/nalind) in [#6127](https://github.com/containers/buildah/pull/6127)
   * Update Buildah issue template to new version and support podman build by [@ninja-quokka](https://github.com/ninja-quokka) in [#6099](https://github.com/containers/buildah/pull/6099)
  
* Vendored: 
   * Update to Go 1.23 for vendoring
   * Vendor in containers/automation_images to v20250324
   * Vendor in dependency golangci/golangci-lint to v2.1.0
   * Vendor in github.com/containernetworking/cni to v1.3.0
   * Vendor in github.com/containers/common to v0.62.2
   * Vendor in github.com/containers/image/v5 to v5.34.2
   * Vendor in github.com/containers/luksy digest to 40bd943
   * Vendor in github.com/opencontainers/selinux to v1.12.0
   * Vendor in github.com/containers/storage to v1.58.0
   * Vendor in github.com/docker/docker to v28.1.0+incompatible
   * Vendor in github.com/go-jose/go-jose/v4 to v4.0.5
   * Vendor in github.com/moby/buildkit to v0.21.0
   * Vendor in github.com/opencontainers/image-spec
   * Vendor in github.com/opencontainers/runc to v1.2.6
   * Vendor in github.com/opencontainers/runtime-spec to v1.2.1 
   * Vendor in github.com/opencontainers/runtime-tools digest to 260e151
   * Vendor in github.com/openshift/imagebuilder digest to e87e4e1
   * Vendor in github.com/spf13/cobra to v1.9.0
   * Vendor in golang.org/x/crypto to v0.37.0
   * Vendor in golang.org/x/net to v0.36.0 [security]
   * Vendor in golang.org/x/sync to v0.11.0
   * Vendor in golang.org/x/sys to v0.30.0
   * Vendor in golang.org/x/term to v0.29.0
   * Vendor in tags.cncf.io/container-device-interface to v1.0.1

* Tests
   * tests/conformance/testdata/Dockerfile.add: update some URLs by [@nalind](https://github.com/nalind) in [#6012](https://github.com/containers/buildah/pull/6012)
   * conformance: make TestCommit and TestConformance parallel by [@flouthoc](https://github.com/flouthoc) in [#5995](https://github.com/containers/buildah/pull/5995)
   * Fix Conformance tests on ARM64 by [@Honny1](https://github.com/Honny1) in [#5990](https://github.com/containers/buildah/pull/5990)
   * [skip-ci] TMT: system tests by [@lsm5](https://github.com/lsm5) in [#5885](https://github.com/containers/buildah/pull/5885)

* Changes to the build infrastructure
   * CI: parallize unit tests by [@flouthoc](https://github.com/flouthoc) in [#5954](https://github.com/containers/buildah/pull/5954)
   * Use tmpfs for integration tests by [@flouthoc](https://github.com/flouthoc) in [#5959](https://github.com/containers/buildah/pull/5959)
   * .cirrus: bump ci resources by [@flouthoc](https://github.com/flouthoc) in [#5979](https://github.com/containers/buildah/pull/5979)
   * cirrus: reduce task timeout by [@Luap99](https://github.com/Luap99) in [#5994](https://github.com/containers/buildah/pull/5994)
   * github: remove cirrus rerun action by [@Luap99](https://github.com/Luap99) in [#6063](https://github.com/containers/buildah/pull/6063)
   * github: check_cirrus_cron work around github bug by [@Luap99](https://github.com/Luap99) in [#6120](https://github.com/containers/buildah/pull/6120)
   * github: disable cron rerun action by [@Luap99](https://github.com/Luap99) in [#6036](https://github.com/containers/buildah/pull/6036)
   * cirrus: make Total Success wait for rootless integration by [@Luap99](https://github.com/Luap99) in [#6130](https://github.com/containers/buildah/pull/6130)
   
* Plus a few minor fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin. We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions! If you haven't joined our community yet, don't wait any longer! Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
