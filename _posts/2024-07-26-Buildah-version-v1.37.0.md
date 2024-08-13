---
title: Buildah version 1.37.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.37.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.37.0](https://github.com/containers/buildah/releases/tag/v1.37.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 39 and Fedora 40.  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon. In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable changes: 
<!--readmore -->
 * When building an image using `buildah build`, the contents of directories marked as volumes (defined by VOLUME instructions), whether as part of the build, or inherited from a base image, will no longer be saved before, and restored after, processing RUN instructions.  The `--compat-volumes` flag can be used to re-enable this behavior.
 * The `config` command now supports the `--healthcheck-start-interval` option, which allows the user to specify the time between health checks during the start period.
 * When `buildah copy` is given the `--from` option, the ownership of items being copied from other images or containers will be preserved by default for better consistency with handling of the `COPY` instruction in Dockerfiles.  The previous behavior can be forced by adding the `--chown=0:0` flag,

This release comprises changes made for v1.37.0 and will be included in Podman v5.2.

## Release Changes

### Changes for v1.37.0
   * Fix secret mounts for environment variables when using chroot isolation by [@jonahbull](https://github.com/jonahbull) in [#5544](https://github.com/containers/buildah/pull/5544)
   * imagebuildah: Support custom image reference lookup for cache push/pull by [@aaronlehmann](https://github.com/aaronlehmann) in [#5532](https://github.com/containers/buildah/pull/5532)
   * The `config` command now supports the `--healthcheck-start-interval` option, which allows the user to specify the time between healthchecks during the start period by [@flouthoc](https://github.com/flouthoc) in [#5472](https://github.com/containers/buildah/pull/5472)
   * A nil pointer reference on that could occur on FreeBSD systems when using the `buildah run` command has been corrected by [@dfr](https://github.com/dfr) in [#5580](https://github.com/containers/buildah/pull/5580)
   * Add some NetBSD support by [@coypoop](https://github.com/coypoop) in [#5559](https://github.com/containers/buildah/pull/5559)
   * When `buildah copy` is given the `--from` option, the ownership of items being copied from other images or containers will be preserved by default for better consistency with handling of the `COPY` instruction in Dockerfiles.  The previous behavior can be forced by adding the `--chown=0:0` flag, by [@nalind](https://github.com/nalind) in [#5597](https://github.com/containers/buildah/pull/5597)
   * Images built using `buildah build` without `--layers=true` will describe their base image in the history entry for the first instruction that was processed, rather than the last instruction by [@nalind](https://github.com/nalind) in [#5595](https://github.com/containers/buildah/pull/5595)
   *  If the “FROM” command was used with a `--platform` option, it is now included when logging the instruction by [@nalind](https://github.com/nalind) in 
[#5599](https://github.com/containers/buildah/pull/5599)
   * Unrecognized values for the `--pull` command line flag are no longer silently treated as if they were "missing" by [@nalind](https://github.com/nalind) in [#5605](https://github.com/containers/buildah/pull/5605)
   * Change default for podman build to --pull missing by [@rhatdan](https://github.com/rhatdan) in [#5583](https://github.com/containers/buildah/pull/5583)
   * When building an image using `buildah build`, the contents of directories marked as volumes (defined by VOLUME instructions), whether as part of the build, or inherited from a base image, will no longer be saved before, and restored after, processing RUN instructions.  The `--compat-volumes` flag can be used to re-enable this behavior by [@nalind](https://github.com/nalind) in [#5604](https://github.com/containers/buildah/pull/5604)
  
### Overall Miscellaneous Changes  
* Documentation:
   * Update godoc for Builder.EnsureContainerPathAs by [@nalind](https://github.com/nalind) in [#5594](https://github.com/containers/buildah/pull/5594)
   * Clarify the definition of --pull options by [@rhatdan](https://github.com/rhatdan) in [#5407](https://github.com/containers/buildah/pull/5407)

* Vendored:
   * Vendor in github.com/containerd/containerd to v1.7.18
   * Vendor in github.com/containernetworking/cni to v1.2.3
   * Vendor in github.com/containers/common to v0.60.0
   * Vendor in github.com/containers/image/v5 to v5.32.0
   * Vendor in github.com/containers/storage to v1.55.0
   * Vendor in github.com/cyphar/filepath-securejoin to v0.3.1
   * Vendor in github.com/docker/docker to v27.1.1+incompatible
   * Vendor in github.com/containers/luksy digest to v0.0.0-20240618143119-a8846e21c08c
   * Vendor in github.com/fsouza/go-dockerclient to v1.11.1
   * Vendor in github.com/onsi/ginkgo/v2 to v2.19.0
   * Vendor in github.com/opencontainers/runc to v1.1.13
   * Vendor in github.com/openshift/imagebuilder to v1.2.14
   * Vendor in github.com/spf13/cobra to v1.8.1
   * Vendor in golang.org/x/crypto to v0.25.0
   * Vendor in golang.org/x/exp digest to v0.0.0-20240613232115-7f521ea00fb8
   * Vendor in golang.org/x/sys to v0.22.0
   * Vendor in golang.org/x/term to v0.22.0
   
* Tests
   * Re-enable two conformance tests by [@nalind](https://github.com/nalind) in [#5566](https://github.com/containers/buildah/pull/5566)
   * tests: set _CONTAINERS_USERNS_CONFIGURED=done for libnetwork by [@nalind](https://github.com/nalind) in [#5574](https://github.com/containers/buildah/pull/5574)

* Changes to the build infrastructure
   * CI: Clarify Debian use for conformance tests by [@cevich](https://github.com/cevich) in [#5538](https://github.com/containers/buildah/pull/5538)
   * [skip-ci] Packit: enable c10s downstream sync by [@lsm5](https://github.com/lsm5) in [#5514](https://github.com/containers/buildah/pull/5514)
   * CI VMs: bump, to debian with cgroups v2 by [@edsantiago](https://github.com/edsantiago) in [#5550](https://github.com/containers/buildah/pull/5550)
   * Cross-build on Fedora by [@cevich](https://github.com/cevich) in [#5572](https://github.com/containers/buildah/pull/5572)
   * CI VMs: bump by [@edsantiago](https://github.com/edsantiago) in [#5600](https://github.com/containers/buildah/pull/5600)
   * CI: use local registry by [@edsantiago](https://github.com/edsantiago) in [#5584](https://github.com/containers/buildah/pull/5584)
   
* Plus a few minor fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin. We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions! If you haven't joined our community yet, don't wait any longer! Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
