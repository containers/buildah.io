---
title: Buildah version 1.35.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.35.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.35.0](https://github.com/containers/buildah/releases/tag/v1.35.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 38 and Fedora 39.  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon.  In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable enhancements: 
<!--readmore -->
 * An `--add-file` flag has been added to the `commit` command to add the file to the committed image.
 * A `--sbom` flag has been added to the `build` and `commit` commands, which allows the created image to be scanned and build contexts.
 *  The `manifest push` command now supports the `--retry` and `--retry-delay` flags.

This release comprises changes made for v1.35.0 and will be included in Podman v5.0.

## Release Changes

### Changes for v1.35.0
   * SELinux relabeling via `:Z` and `:z` on file systems that do not support labels like NFS are now ignored by @rhatdan in #5197
   * An `--add-file` option has been added to the `commit` command to add the file to the committed image by @nalind in #5226
   * When building using Heredoc notation, Buildah now correctly bursts the layer cache if the HereDoc content is changed by @flouthoc in #5261
   * The `buildah mkcw` command now accepts an `--add-file` option, which can be used to add a file to the committed image without modifying the working container which is being committed by @nalind in #5252
   * The `buildah commit` and `buildah build` commands now recognize `--sbom` and related options, which can be used to scan the image that is being created.  The scanner's output can be added to the image or saved to the local disk by @nalind in #5279
   * An interpreter/shebang is now honored in HereDoc by @flouthoc in #5255
   * The `no-dereference` option has been added as a valid mount option by @rhatdan in #5299
   * The `manifest push` command now supports the `--retry` and `--retry-delay` flags by @flouthoc in #5315
   * Buildah now sets the maximum ulimits, nofile and nproc values by default by @rhatdan in #5275
   * The build output now shows a progress bar while pushing and pulling images by @flouthoc in #5314
   * `buildah manifest add` now accepts an `--artifact` option, which can create artifact manifests for arbitrary files and add those artifact manifests to an image index by @nalind in #5301
   * `buildah manifest annotate` now accepts a `--index` option, indicating that `--annotation` values should be added to the image index rather than an item listed in an image index by @nalind in #5301
   * Error messages when using the `--sbom` related flags have been tidied up by @nalind in #5288
   * Building with `--all-platforms` will now refrain from building for platforms with OS or Architecture values that are empty or set to the value "unknown".  Additionally, "Architecture" values that are not recognized by the Go compiler will also be skipped by @nalind in #5335
   * Changed the base image of the official Buildah image to fedora-minimal to reduce its size by @isker in #5347
   * The `build --pull=false` command no longer pulls the image by @rhatdan in #5354
   * Default values for `--retry` and `--retry-delay` can be set in containers.conf by @rhatdan in #5345
   * The `manifest add` command now complains if `--artifact-*` options are used without the `--artifact` option by @nalind in #5366

### Overall Miscellaneous Changes  
* Documentation:
   * [CI:DOCS] Document use of containers-transports values in buildah by @rhatdan in #5230
   * [CI:DOCS] move footnotes to where they're applicable by @edsantiago in #5305
   * [CI:DOCS] Revert "Reduce official image size" by @cevich in #5350
   * [CI:DOCS] docs: correct default authfile path by @rhatdan in #5319
   * [CI:DOCS] Add comment re: Total Success task name by @cevich in #5342
   * Use reversed logo for dark theme in README by @Sea-n in #5287
   
* Vendored: 
   * Vendor in github.com/containerd/containerd v1.7.13
   * Vendor in github.com/containernetworking/plugins v1.4.0
   * Vendor in github.com/containers/common v0.58.0
   * Vendor in github.com/containers/image/v5 v5.30.0
   * Vendor in github.com/containers/luksy v0.0.0-20240212203526-ceb12d4fd50c
   * Vendor in github.com/containers/storage v1.53.0
   * Vendor in github.com/fsouza/go-dockerclient v1.10.1
   * Vendor in github.com/moby/buildkit v0.12.5
   * Vendor in github.com/onsi/gomega v1.31.1
   * Vendor in github.com/opencontainers/image-spec v1.1.0
   * Vendor in github.com/opencontainers/runc v1.1.11
   * Vendor in github.com/openshift/imagebuilder v1.2.6
   * Vendor in github.com/stretchr/testify v1.9.0
   * Vendor in go.etcd.io/bbolt v1.3.9
   * Vendor in golang.org/x/crypto v0.21.0
   * Vendor in golang.org/x/sync v0.6.0
   * Vendor in golang.org/x/term v0.18.0

* Tests
   * tests: skip_if_no_unshare(): check for --setuid by @edsantiago in #5360
   * Add a conformance test for copying to a mounted prior stage by @nalind in #5375
   * conformance tests: don't break on trailing zeroes in layer blobs by @nalind in #5386

* Changes to the build infrastucture
  * Fix a build break on FreeBSD by @dfr in #5293

* Plus a few minor fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
