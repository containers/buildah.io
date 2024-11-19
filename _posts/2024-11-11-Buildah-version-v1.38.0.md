---
title: Buildah version 1.38.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.38.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.38.0](https://github.com/containers/buildah/releases/tag/v1.38.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 40 and Fedora 41.  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon. In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable changes: 
<!--readmore -->
 * `ADD` commands now use configured CA certificates with HTTPS
 * Git sources can now be used in Containerfile `ADD` commands
 * Fixes for CVE-2024-9407 and CVE-2024-9675

This release comprises changes made for v1.38.0 and will be included in Podman v5.3.

## Release Changes
### Changes for v1.38.0
   * `buildah add` and ADD instructions used with `buildah build` now use configured CA certificates and retry settings when retrieving contents from HTTPS locations by [@nalind](https://github.com/nalind) in [#5646](https://github.com/containers/buildah/pull/5646)
   * On Debian/Ubuntu, add installation of libbtrfs-dev and libdevmapper-dev by [@jelmer](https://github.com/jelmer) in [#5541](https://github.com/containers/buildah/pull/5541)
   * COPY and ADD instructions being processed by `buildah build` will now be handled correctly if items matched by source location globs have names that include characters that are treated as special when globbing by [@nalind](https://github.com/nalind) in [#5676](https://github.com/containers/buildah/pull/5676)
   * A retry mechanism process was added to the committing process to local storage to help with parallelization by [@nalind](https://github.com/nalind) in [#5686](https://github.com/containers/buildah/pull/5686)
   * Fixed a nil pointer dereference on FreeBSD by [@dfr](https://github.com/dfr) in [#5694](https://github.com/containers/buildah/pull/5694)
   * `buildah build` now expands "**" path components in source locations in ADD and COPY instructions as referring to any subdirectory by [@nalind](https://github.com/nalind) in [#5688](https://github.com/containers/buildah/pull/5688)
   * Buildah now uses the pasta --map-guest-addr option by default which is used for the host.containers.internal entry to allow the container to reach the host by default. by [@Luap99](https://github.com/Luap99) in [#5724](https://github.com/containers/buildah/pull/5724)
   * Add support for git sources in the Containerfile `ADD` command by [@danishprakash](https://github.com/danishprakash) in [#5438](https://github.com/containers/buildah/pull/5438)
   * `buildah manifest add --artifact` no longer fails if it's invoked with multiple file arguments.  All of the files should be added to a single artifact manifest which should then be added to the image index being updated by [@nalind](https://github.com/nalind) in [#5728](https://github.com/containers/buildah/pull/5728)
   * If a target platform for `buildah build` is not specified with one of the `--platform`, `--os`, or `--arch` flags, but a `TARGETPLATFORM` build argument has been set with `--build-arg`, its value will be used as though it had been specified to `--platform` by [@nalind](https://github.com/nalind) in [#5731](https://github.com/containers/buildah/pull/5731)
   * The `buildah build` `--compat-excludes` flag will now has the intended effect when used in combination with `--layers`. by [@nalind](https://github.com/nalind) in [#5729](https://github.com/containers/buildah/pull/5729)
   * buildah container images will now attempt to use the qemu-user-static binaries they include, if they also include configuration for them, for running binaries built for non-native architectures by [@nalind](https://github.com/nalind) in [#5732](https://github.com/containers/buildah/pull/5732)
   * Including a file with the `security.ima` xattr set as a non-root user will no longer fail as the xattr could not be set by [@mheon](https://github.com/mheon) in [#5741](https://github.com/containers/buildah/pull/5741)
   * Fixed a duplicate condition issue by [@cuishuang](https://github.com/cuishuang) in [#5745](https://github.com/containers/buildah/pull/5745)
   * CVE-2024-9407: validate "bind-propagation" flag settings in run commands by [@nalind](https://github.com/nalind) in [#5761](https://github.com/containers/buildah/pull/5761)
   * `buildah manifest push --all` is now true by default to match Podman by [@k9withabone](https://github.com/k9withabone) in [#5755](https://github.com/containers/buildah/pull/5755)
   * Fixed CVE-2024-9675 which allowed arbitrary paths from the host to be mounted into a build container using the `--mount type=cache` argument to the `RUN` instruction in Dockerfiles. by [@mheon](https://github.com/mheon) in [#5778](https://github.com/containers/buildah/pull/5778)
   * Add support for COPY --exclude and ADD --exclude options by [@rhatdan](https://github.com/rhatdan) in [#5733](https://github.com/containers/buildah/pull/5733)
   * Newlines were added at the end of some printed error messages to make them more readable by [@nalind](https://github.com/nalind) in [#5753](https://github.com/containers/buildah/pull/5753)
   * RUN instructions which use the --mount flag with a relative "target" path no longer trigger an error if the current stage does not have a defined working directory by [@nalind](https://github.com/nalind) in [#5798](https://github.com/containers/buildah/pull/5798)
      
### Overall Miscellaneous Changes  
* Documentation:
   * buildah-build.1.md: expand the --layer-label description by [@nalind](https://github.com/nalind) in [#5701](https://github.com/containers/buildah/pull/5701)
   * update some godocs, use 0o to prefix an octal in a comment by [@nalind](https://github.com/nalind) in [#5702](https://github.com/containers/buildah/pull/5702)
   * Update tutorials to keep up with API changes in storage by [@nalind](https://github.com/nalind) in [#5665](https://github.com/containers/buildah/pull/5665)
   * Document how entrypoint is configured in buildah config by [@rhatdan](https://github.com/rhatdan) in [#5734](https://github.com/containers/buildah/pull/5734)
   * buildah-manifest-create.1: Fix manpage section by [@siretart](https://github.com/siretart) in [#5757](https://github.com/containers/buildah/pull/5757)
   * Document that zstd:chunked is downgraded to zstd when encrypting by [@mtrmac](https://github.com/mtrmac) in [#5759](https://github.com/containers/buildah/pull/5759)
   * Document more buildah build --secret options by [@nalind](https://github.com/nalind) in [#5784](https://github.com/containers/buildah/pull/5784)
   
* Vendored: 
   * Vendor in containers/automation_images to v20241010
   * Vendor in github.com/containers/common to v0.61.0
   * Vendor in github.com/containers/image/v5 to v5.33.0
   * Vendor in github.com/containers/luksy digest to e2530d6
   * Vendor in github.com/containers/storage to v1.56.0
   * Vendor in github.com/cyphar/filepath-securejoin to v0.3.4
   * Vendor in github.com/docker/docker to v27.3.1+incompatible
   * Vendor in github.com/fsouza/go-dockerclient to v1.12.0
   * Vendor in github.com/moby/buildkit to v0.17.1 
   * Vendor in github.com/onsi/ginkgo/v2 to v2.19.1
   * Vendor in github.com/onsi/gomega to v1.34.1
   * Vendor in github.com/opencontainers/runc to v1.2.1
   * Vendor in github.com/opencontainers/runtime-tools digest to 6c9570a
   * Vendor in github.com/opencontainers/selinux to v1.11.1
   * Vendor in github.com/openshift/imagebuilder to v1.2.15
   * Vendor in golang.org/x/crypto to v0.29.0
   * Vendor in golang.org/x/exp digest to f66d83c 
   * Vendor in golang.org/x/sys to v0.27.0
   * Vendor in golang.org/x/term to v0.26.0
   
* Tests
   * Drop the e2e test suite by [@nalind](https://github.com/nalind) in [#5668](https://github.com/containers/buildah/pull/5668)
   * conformance tests: use mirror.gcr.io for most images by [@nalind](https://github.com/nalind) in [#5673](https://github.com/containers/buildah/pull/5673)
   * unit tests: use test-specific policy.json and registries.conf by [@nalind](https://github.com/nalind) in [#5672](https://github.com/containers/buildah/pull/5672)
   * conformance: move weirdly-named files out of the repository by [@nalind](https://github.com/nalind) in [#5684](https://github.com/containers/buildah/pull/5684)
   * tests: add quotes to names by [@Luap99](https://github.com/Luap99) in [#5765](https://github.com/containers/buildah/pull/5765)
   * Integration tests: run git daemon on a random-but-bind()able port by [@nalind](https://github.com/nalind) in [#5783](https://github.com/containers/buildah/pull/5783)
   * tests: mkcw: bug fixes, refactor by [@edsantiago](https://github.com/edsantiago) in [#5802](https://github.com/containers/buildah/pull/5802)
   * tests: sbom: never write to cwd by [@edsantiago](https://github.com/edsantiago) in [#5803](https://github.com/containers/buildah/pull/5803)
   * tests: blobcache: use unique image name by [@edsantiago](https://github.com/edsantiago) in [#5801](https://github.com/containers/buildah/pull/5801)
   * tests: bud: make parallel-safe by [@edsantiago](https://github.com/edsantiago) in [#5804](https://github.com/containers/buildah/pull/5804)
   * tests/tools: update golangci-lint to v1.61.0 by [@Luap99](https://github.com/Luap99) in [#5821](https://github.com/containers/buildah/pull/5821)
   
* Changes to the build infrastructure
   * CI VMs: bump f40 -> f41 by [@edsantiago](https://github.com/edsantiago) in [#5820](https://github.com/containers/buildah/pull/5820)
   * CI: enable the gofumpt and whitespace linters by [@nalind](https://github.com/nalind) in [#5689](https://github.com/containers/buildah/pull/5689)
   * gofix, gofmt the code, add gofmt linter by [@kolyshkin](https://github.com/kolyshkin) in [#5680](https://github.com/containers/buildah/pull/5680)
   * make vendor-in-container: use the caller's Go cache if it exists by [@nalind](https://github.com/nalind) in [#5667](https://github.com/containers/buildah/pull/5667)
   * Use Epoch: 2 and respect the epoch in dependencies. by [@jnovy](https://github.com/jnovy) in [#5654](https://github.com/containers/buildah/pull/5654)
   * New VMs by [@edsantiago](https://github.com/edsantiago) in [#5703](https://github.com/containers/buildah/pull/5703)
   * Update to go 1.22 by [@Luap99](https://github.com/Luap99) in [#5715](https://github.com/containers/buildah/pull/5715)
   * Packit: Enable sidetags for bodhi updates by [@lsm5](https://github.com/lsm5) in [#5730](https://github.com/containers/buildah/pull/5730)
   * Packit: constrain koji job to fedora package to avoid dupes by [@lsm5](https://github.com/lsm5) in [#5774](https://github.com/containers/buildah/pull/5774)
   * Add a validation script for Makefile $(SOURCES) by [@nalind](https://github.com/nalind) in [#5704](https://github.com/containers/buildah/pull/5704)
   
* Plus a few minor fixes.


## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin. We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions! If you haven't joined our community yet, don't wait any longer! Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
