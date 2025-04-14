---
title: Buildah version 1.39.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.39.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.39.0](https://github.com/containers/buildah/releases/tag/v1.39.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 40 and Fedora 41.  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon. In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable changes: 
<!--readmore -->
 * An `--artifact-annotation` option has been added to the `manifest add` command to allow for annotation of the artifact manifest.
* Cache now works when additional build context is used as the source of --mount.
* The `build` command has two new options, --security-opt mask and unmask.
* The `buildah build` RUN instructions and `buildah run` command can now refer to images with the `from` argument when using the `--mount=type=cache` option.

This release comprises changes made for v1.39.0 and will be included in Podman v5.4.

## Release Changes
### Changes for v1.39.0
   * executor: allow to specify --no-pivot-root by [@giuseppe](https://github.com/giuseppe) [#5838](https://github.com/containers/buildah/pull/5838)
   * The `buildah manifest add` command now includes a `--artifact-annotation` flag which can be used to add an annotation to the artifact manifest which is generated and then added to the image index. by [@nalind](https://github.com/nalind) [#5854](https://github.com/containers/buildah/pull/5854)
   * The `buildah build` or `buildah run` with `--isolation chroot` will now default to using pivot_root() internally, unless the `--no-pivot` CLI flag is used. by [@nalind](https://github.com/nalind) [#5874](https://github.com/containers/buildah/pull/5874)
   * Cache now works when additional build context is used as the source of --mount by [@flouthoc](https://github.com/flouthoc) [#5693](https://github.com/containers/buildah/pull/5693)
   * Allow cache mounts to be stages and additional build contexts by [@nalind](https://github.com/nalind) [#5897](https://github.com/containers/buildah/pull/5897)
   * The `build` command has two new options, --security-opt mask and unmask.  Refer to the `build(1) man page for more information by [@rhatdan](https://github.com/rhatdan) [#5883](https://github.com/containers/buildah/pull/5883)
   * Add more checks to the --mount flag parsing logic by [@nalind](https://github.com/nalind) [#5925](https://github.com/containers/buildah/pull/5925)
   * Refactor: replace golang.org/x/exp with stdlib by [@Juneezee](https://github.com/Juneezee) [#5937](https://github.com/containers/buildah/pull/5937)
   * Changes were made to more thoroughly unmount images by [@nalind](https://github.com/nalind) [#5924](https://github.com/containers/buildah/pull/5924)
   * The `buildah build` RUN instructions and `buildah run` command can now refer to images with the `from` argument when using the `--mount=type=cache` option. by [@nalind](https://github.com/nalind) [#5934](https://github.com/containers/buildah/pull/5934)
   * The `build` and `run` commands now record hash or digest in the image history for sources used in `--mount`. by [@flouthoc](https://github.com/flouthoc) [#5691](https://github.com/containers/buildah/pull/5691)
      
### Overall Miscellaneous Changes  
* Documentation:
   * Fixed a broken doc link by [@cheesesashimi](https://github.com/cheesesashimi) [#5936](https://github.com/containers/buildah/pull/5936)
  
* Vendored: 
   * Vendor in github.com/containers/common to v0.62.0
   * Vendor in github.com/containers/image to v5.34.0
   * Vendor in github.com/containers/luksy digest to a3a812d
   * Vendor in github.com/containers/ocicrypt to v1.2.1
   * Vendor in github.com/containers/storage to v1.57.1
   * Vendor in github.com/cyphar/filepath-securejoin to v0.3.6
   * Vendor in github.com/docker/docker to v27.5.1
   * Vendor in github.com/moby/buildkit to v0.19.0
   * Vendor in github.com/moby/sys/capability to v0.4.8
   * Vendor in github.com/opencontainers/runc to v1.2.4
   * Vendor in github.com/opencontainers/runtime-tools digest to f7e3563b0271
   * Vendor in github.com/stretchr/testify to v1.10.0
   * Vendor in github.com/vbatts/tar-split to v0.11.7.
   * Vendor in golang.org/x/crypto to v0.32.0
   * Vendor in golang.org/x/exp digest to 7d7fa50e5329
   * Vendor in golang.org/x/net to v0.34.0

* Tests
   * Make _prefetch() parallel-safe by [@edsantiago](https://github.com/edsantiago) [#5841](https://github.com/containers/buildah/pull/5841)
   * Parallelize some bats tests by [@edsantiago](https://github.com/edsantiago) [#5552](https://github.com/containers/buildah/pull/5552)   
   * copy-preserving-extended-attributes: use a different base image by [@nalind](https://github.com/nalind) [#5901](https://github.com/containers/buildah/pull/5901)
   * chroot mount flags integration test: copy binaries by [@nalind](https://github.com/nalind) [#5926](https://github.com/containers/buildah/pull/5926)

* Changes to the build infrastructure
   * CI VMs: bump again by [@edsantiago](https://github.com/edsantiago) [#5833](https://github.com/containers/buildah/pull/5833)
   * Finish updating to go 1.22 by [@nalind](https://github.com/nalind) [#5835](https://github.com/containers/buildah/pull/5835)
   * Makefile cleanups by [@kolyshkin](https://github.com/kolyshkin) [#5832](https://github.com/containers/buildah/pull/5832)
   * Makefile: list sources via find conditionally by [@danishprakash](https://github.com/danishprakash) [#5807](https://github.com/containers/buildah/pull/5807)
   * Packit: f39 and rhel cleanups by [@lsm5](https://github.com/lsm5) [#5849](https://github.com/containers/buildah/pull/5849)
   * CI: remove some inter-job dependencies, run cross-compile task with make -j, use /tmp for Go build cache by [@nalind](https://github.com/nalind) [#5856](https://github.com/containers/buildah/pull/5856)
   * New VM Images by [@Luap99](https://github.com/Luap99) [#5900](https://github.com/containers/buildah/pull/5900)
   * RPM: use default gobuild macro on RHEL by [@lsm5](https://github.com/lsm5) [#5938](https://github.com/containers/buildah/pull/5938)
   * CI, .cirrus: parallelize containerized integration by [@flouthoc](https://github.com/flouthoc) [#5947](https://github.com/containers/buildah/pull/5947)
   
* Plus a few minor fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin. We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions! If you haven't joined our community yet, don't wait any longer! Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
