---
title: Buildah version 1.42.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.42.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.42.0](https://github.com/containers/buildah/releases/tag/v1.42.0), which is now available from GitHub for any Linux distro.  We are shipping this release on [Fedora 42](https://bodhi.fedoraproject.org/updates/FEDORA-2025-8a248ee4f4)  and [Fedora 43](https://bodhi.fedoraproject.org/updates/FEDORA-2025-beb4c9a336).  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon. In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable changes: 
<!--readmore -->
 * The meaning of `--pull` now emulates Docker's `--pull=always`
 * Destination locations for several commands that now end with a `/.` are treated as directories.
 * The `--imagestore` option can now be used when configuring storage.
 * The `--transient-store` option stores metadata about containers under the storage state directory.  See the buildah (1) man page for details.

This release comprises changes made for v1.42.0 and will be included in Podman v5.7.


## Release Changes
### Changes for v1.42.0
   * Restore the meaning of `--pull` (without argument), similar to the docker behavior: now defaults to `--pull=always` by [@Romain-Geissler-1A](https://github.com/Romain-Geissler-1A) in [#6300](https://github.com/containers/buildah/pull/6300)
   * Exclude pulled up parent directories at commit-time by [@nalind](https://github.com/nalind) in [#6296](https://github.com/containers/buildah/pull/6296)
   * Only suppress "noted" items when not squashing by [@nalind](https://github.com/nalind) in [#6302](https://github.com/containers/buildah/pull/6302)
   * History should note unset-label, timestamp, and rewrite-timestamp by [@nalind](https://github.com/nalind) in [#6315](https://github.com/containers/buildah/pull/6315)
   * --mount=type=bind now does ignores modtime when looking for cache candidates by [@flouthoc](https://github.com/flouthoc) in [#6311](https://github.com/containers/buildah/pull/6311)
   * Destination locations specified for `buildah add` and `buildah copy`, and in ADD and COPY instructions for `buildah build`, that end with "/." are now always expected to be directories by [@nalind](https://github.com/nalind) in [#6310](https://github.com/containers/buildah/pull/6310)
   * Run: reap stray processes by [@nalind](https://github.com/nalind) in [#6307](https://github.com/containers/buildah/pull/6307)
   * imagebuildah.StageExecutor.Execute: commit more "no instructions" cases by [@nalind](https://github.com/nalind) in [#6314](https://github.com/containers/buildah/pull/6314)
   * Rework how we decide what to filter out of layer diffs by [@nalind](https://github.com/nalind) in [#6332](https://github.com/containers/buildah/pull/6332)
   * Mount image fails with imagestores by [@nalind](https://github.com/nalind) in [#6340](https://github.com/containers/buildah/pull/6340)
   * Losen the dependency on go-connections/tlsconfig by [@mtrmac](https://github.com/mtrmac) in [#6328](https://github.com/containers/buildah/pull/6328)
   * The global `--imagestore` flag can now be used when configuring storage by [@nalind](https://github.com/nalind) in [#6341](https://github.com/containers/buildah/pull/6341)
   * The global `--transient-store` flag is now recognized by [@nalind](https://github.com/nalind) in [#6346](https://github.com/containers/buildah/pull/6346)
   * FROM instructions which reference images using both a tag and a digest no longer trigger errors in `buildah build` with `--all-platforms`: the tag portion of the reference will be ignored by [@nalind](https://github.com/nalind) in [#6353](https://github.com/containers/buildah/pull/6353)
   * The chroot isolation handler should now correctly use $PATH to find the binary to run when RUN instructions express the command to run in exec form, and which do not do so using an absolute path by [@nalind](https://github.com/nalind) in [#6378](https://github.com/containers/buildah/pull/6378)
   * Parent directories created for mounts used by `buildah run` or by RUN instructions in `buildah build` will be world-readable again by [@nalind](https://github.com/nalind) in [#6381](https://github.com/containers/buildah/pull/6381)
   * commit: always return the config digest as the image ID by [@nalind](https://github.com/nalind) in [#6426](https://github.com/containers/buildah/pull/6426)
   * copier: ignore user.overlay.* xattrs by [@nalind](https://github.com/nalind) in [#6429](https://github.com/containers/buildah/pull/6429)
   * Include the Sequoia crypto backend, and run integration tests with it by [@mtrmac](https://github.com/mtrmac) in [#6390](https://github.com/containers/buildah/pull/6390)
   * build,add: add support for corporate proxies by [@userid0x0](https://github.com/userid0x0) in [#6274](https://github.com/containers/buildah/pull/6274)

* Documentation:
   * Adding mohanboddu as community manager to MAINTAINERS.md by [@mohanboddu](https://github.com/mohanboddu) in [#6339](https://github.com/containers/buildah/pull/6339)
   
* Vendored (Note, storage, image and common move to go.podman.io during this release): 
   * Vendor github.com/containers/common to v0.64.1 
   * Vendor github.com/containers/luksy digest to 2cf5bc9 
   * Vendor github.com/containers/image/v5 to v5.36.1 
   * Vendor github.com/containers/storage to v1.59.1 
   * Vendor github.com/cyphar/filepath-securejoin to v0.4.1
   * Vendor github.com/docker/docker to v28.5.1+incompatible
   * Vendor github.com/docker/go-connections to v0.6.0
   * Vendor github.com/fsouza/go-dockerclient to v1.12.2
   * Vendor github.com/moby/buildkit to v0.25.1
   * Vendor github.com/opencontainers/cgroups to v0.0.5
   * Vendor github.com/opencontainers/runc to v1.3.2
   * Vendor github.com/openshift/imagebuilder to v1.2.19
   * Vendor github.com/seccomp/libseccomp-golang to v0.11.1
   * Vendor github.com/stretchr/testify to v1.11.1
   * Vendor github.com/spf13/cobra to v1.10.1
   * Vendor github.com/spf13/pflag to v1.0.10
   * Vendor github.com/ulikunitz/xz to v0.5.15 
   * Vendor go.etcd.io/bbolt to v1.4.3
   * Vendor go.podman.io/common to v0.66.0
   * Vendor go.podman.io/image/v5 to v5.38.0
   * Vendor go.podman.io/storage to v1.61.0
   * Vendor golang.org/x/crypto to v0.43.0
   * Vendor golang.org/x/sys to v0.37.0
   * Vendor golang.org/x/term to v0.34.0

* Tests:
   * CI: make runc tests non-blocking by [@nalind](https://github.com/nalind) in [#6286](https://github.com/containers/buildah/pull/6286)
   * Make some test files different from each other by [@nalind](https://github.com/nalind) in [#6405](https://github.com/containers/buildah/pull/6405)
   
* Changes to the build infrastructure:
   * Switch common, storage and image to monorepo. by [@jankaluza](https://github.com/jankaluza) in [#6356](https://github.com/containers/buildah/pull/6356)
   * Update to Go 1.24 by [@nalind](https://github.com/nalind) in [#6380](https://github.com/containers/buildah/pull/6380)
   * .cirrus.yml: Test Vendoring bump golang by [@flouthoc](https://github.com/flouthoc) in [#6386](https://github.com/containers/buildah/pull/6386)
   
New Contributors:
   * [@Romain-Geissler-1A](https://github.com/Romain-Geissler-1A) first contribution in [#6300](https://github.com/containers/buildah/pull/6300)
   * [@mohanboddu](https://github.com/mohanboddu) made their first contribution in [#6339](https://github.com/containers/buildah/pull/6274)
   * [@jankaluza](https://github.com/jankaluza) made their first contribution in [#6356](https://github.com/containers/buildah/pull/6274)
   * [@userid0x0](https://github.com/userid0x0) made their first contribution in [#6274](https://github.com/containers/buildah/pull/6274)

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin. We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions! If you haven't joined our community yet, don't wait any longer! Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
