---
title: Buildah version 1.31.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.31.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.31.0](https://github.com/containers/buildah/releases/tag/v1.31.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 37, Fedora 38, and Fedora 39.  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon.  In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable enhancements: 
<!--readmore -->
 * Buidlah now supports pasta as network mode like podman.  
 * Slirp4netns now uses the options from containers.conf and uses ipv6 by default.
 * Buildah now reads the default_rootless_network_cmd containers.conf option to get the default rootless network program.
 * The device mapper storage driver support has been removed.

This release comprises changes made for v1.31.0 and will be included in Podman v4.5.

## Release Changes

### Changes for v1.31.0
   * Revert "buildah image should not enable fuse-overlayfs for rootful mode" by @flouthoc in [#4722](https://github.com/containers/buildah/pull/4722)
   * Add support for relabel bind mount option by @danishprakash in [#4705](https://github.com/containers/buildah/pull/4705)
   * build: --platform must accept only arch by @flouthoc in [#4757](https://github.com/containers/buildah/pull/4757)
   * parse: filter edge-case for podman-remote by @flouthoc in [#4765](https://github.com/containers/buildah/pull/4765)
   * Fix an overflow on retries on container name conflicts by @mtrmac in [#4752](https://github.com/containers/buildah/pull/4752)
   * Manifest, push: use source as destination if not specified by @flouthoc in [#4767](https://github.com/containers/buildah/pull/4767)
   * When doing a mount in the run command, remove the path only if they didnt pre-exist by @flouthoc in [#4755](https://github.com/containers/buildah/pull/4755)
   * Accept required flag for a secret without value by @flouthoc in [#4791](https://github.com/containers/buildah/pull/4791)
   * Build: The volumes are now validated on the backend rather than the frontend by @flouthoc in [#4792](https://github.com/containers/buildah/pull/4792)
   * Problematic calls to  prctl(PR_SET_PDEATHSIG) have been dropped from the Go code by @giuseppe in [#4790](https://github.com/containers/buildah/pull/4790)
   * References to registry.centos.org have been removed since it is decommissioned by @flouthoc in [#4819](https://github.com/containers/buildah/pull/4819)
   * Labels defined for the build process are now applied to only the final stage by @flouthoc in [#4817](https://github.com/containers/buildah/pull/4817)
   * The ‘image_copy_tmp_dir’ field from containers.conf is now used if ENV: TMPDIR is not found by @flouthoc in [#4844](https://github.com/containers/buildah/pull/4844)
   * When run with debug-level logging enabled, the buildah binary will log the set of effective capabilities at startup by @nalind in [#4836](https://github.com/containers/buildah/pull/4836)
   * The device mapper storage driver support has been removed by @kolyshkin in [#4832](https://github.com/containers/buildah/pull/4832)
   * The hostname is now added to /etc/hosts when running with host network by @Luap99 in [#4869](https://github.com/containers/buildah/pull/4869)
   * Buidlah now supports pasta as network mode like podman.  Also, Slirp4netns now uses the options from containers.conf and uses ipv6 by default by @Luap99 in [#4877](https://github.com/containers/buildah/pull/4877)
   *  Buildah now reads the default_rootless_network_cmd containers.conf option to get the default rootless network program by @Luap99 in [#4889](https://github.com/containers/buildah/pull/4889)

### Overall Miscellaneous Changes  
* Documentation:
   * Clarify the need for qemu-user-static package by @rhatdan in [#4738](https://github.com/containers/buildah/pull/4738)
   * Update the demos README file to fix minor typos by @pixdrift in [#4781](https://github.com/containers/buildah/pull/4781)
   * Update comment to remove ambiguity by @cevich in [#4849](https://github.com/containers/buildah/pull/4849)
   * Renovate: Don't touch fragile test stuffs by @cevich in [#4856](https://github.com/containers/buildah/pull/4856)
   * Add a warning to build --secret docs by @rijenkii in [#4823](https://github.com/containers/buildah/pull/4823)

* Vendored:
   * Vendor in github.com/containerd/containerd v1.7.2
   * Vendor in github.com/containers/common v0.55.1
   * Vendor in github.com/containers/image/v5 v5.26.1
   * Vendor in github.com/containers/storage v1.48.0
   * Vendor in github.com/docker/docker v24.0.2
   * Vendor in github.com/docker/distribution to v2.8.2
   * Vendor in github.com/onsi/gomega v1.27.8
   * Vendor in github.com/opencontainers/runc v1.1.7
   * Vendor in github.com/opencontainers/runtime-spec v1.1.0-rc.3
   * Vendor in github.com/openshift/imagebuilder v1.2.5
   * Vendor in github.com/sirupsen/logrus v1.9.3
   * Vendor in github.com/stretchr/testify v1.8.4
   * Vendor in golang.org/x/crypto v0.10.0
   * Vendor in golang.org/x/sync v0.3.0
   * Vendor in golang.org/x/term v0.9.0

* Tests:
   * Add smoke tests for encryption CLI helpers by @mtrmac in [#4745](https://github.com/containers/buildah/pull/4745)
   * Use debian instead of docker.io/library/debian:testing-slim when testing by @flouthoc in [#4807](https://github.com/containers/buildah/pull/4807)
   * The intermediate-images inherit-label test has been made debuggable by @edsantiago in [#4837](https://github.com/containers/buildah/pull/4837)
   * Fix the transition test to work with the latest selinux policy by @rhatdan in [#4829](https://github.com/containers/buildah/pull/4829)

* Changes to the build infrastructure:
   * Fix a test broken by the renovatebot by @edsantiago in [#4812](https://github.com/containers/buildah/pull/4812)
   * Support testing w/ podman-next COPR packages by @cevich in [#4830](https://github.com/containers/buildah/pull/4830)
   * Makefile: don't show sed invocations by @kolyshkin in [#4841](https://github.com/containers/buildah/pull/4841)
   * Makefile: increase conformance timeout by @flouthoc in [#4760](https://github.com/containers/buildah/pull/4760)   * Packit: add jobs for downstream Fedora package builds by @lsm5 in [#4870](https://github.com/containers/buildah/pull/4870)
   * Fix a meta task failing to find commits by @cevich in [#4773](https://github.com/containers/buildah/pull/4773)
   * Explicitly ref. quay images for CI by @cevich in [#4828](https://github.com/containers/buildah/pull/4828)

* Plus several minor fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
