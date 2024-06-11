---
title: Buildah version 1.36.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.36.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.36.0](https://github.com/containers/buildah/releases/tag/v1.36.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 39 and Fedora 40.  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon. In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable changes: 
<!--readmore -->
 * The `--device` option has been added to the `buildah run` command.
 * CVE-2024-3727 and CVE-2024-1753 have been addressed.
 * Improvements to the Heredoc functionality.

This release comprises changes made for v1.36.0 and will be included in Podman v5.1.

## Release Changes

### Changes for v1.36.0
   * fix /etc/hosts and resolv.conf setup with network configs by @Luap99 in  [#5409](https://github.com/containers/buildah/pull/5409)
   * CVE-2024-1753 container escape fix by @TomSweeneyRedHat in  [#5411](https://github.com/containers/buildah/pull/5411)
   * Makefile - instead of calling as directly, use it from env var by @rahilarious in  [#5436](https://github.com/containers/buildah/pull/5436)
   * `buildah run` now accepts a `--device` option. The `--device` option can now accept names of devices that are specified using CDI (container device interface). by @nalind in  [#5443](https://github.com/containers/buildah/pull/5443)
   * Makefile: softcode strip, use it from env var by @rahilarious in  [#5446](https://github.com/containers/buildah/pull/5446)
   * Fix caching when mounting a cached stage with COPY/ADD by @aaronlehmann in  [#5445](https://github.com/containers/buildah/pull/5445)
   * source-push: add support for --digestfile by @flouthoc in  [#5444](https://github.com/containers/buildah/pull/5454)
   * heredoc: honor inline COPY irrespective of .containerignore file by @flouthoc in  [#5459](https://github.com/containers/buildah/pull/5459)
   * Address CVE-2024-3727, an image library flaw by @TomSweeneyRedHat in  [#5523](https://github.com/containers/buildah/pull/5523)
   * Setting --arch should set the TARGETARCH build arg by @rhatdan in  [#5478](https://github.com/containers/buildah/pull/5478)
   * Add release note template to split dependency chores by @der-eismann in  [#5463](https://github.com/containers/buildah/pull/5463)
   * Don't leak temp files on failures by @rhatdan in  [#5527](https://github.com/containers/buildah/pull/5527)
   * Environment variables referenced in RUN instructions that use heredoc syntax will now be evaluated by the command being invoked rather than by the builder by @nalind in  [#5473](https://github.com/containers/buildah/pull/5473)

### Overall Miscellaneous Changes  
* Documentation:
   * fix links to containerignore doc by @Pvlerick in  [#5402](https://github.com/containers/buildah/pull/5402)
   * [CI:DOCS] Migrate buildah container image by @cevich in  [#5384](https://github.com/containers/buildah/pull/5384)
   * Update install.md by @onlykzy in  [#5457](https://github.com/containers/buildah/pull/5457)
   * [CI:DOCS] Add golang 1.21 update warning by @cevich in  [#5437](https://github.com/containers/buildah/pull/5437)
   * Fix buildah prune --help examples by @naskya in  [#5534](https://github.com/containers/buildah/pull/5534)
   
* Vendored: 
   * Vendor in github/containers.common to v0.59.0
   * Vendor in github.com/containers/image/v5 to v5.31.0
   * Vendor in github.com/containers/luksy to 84b50f50f3ee
   * Vendor in github.com/containers/ocicrypt to v1.1.10
   * Vendor in github.com/cyphar/filepath-securejoin to v0.2.5
   * Vendor in github.com/docker/docker to v26.1.3+incompatible
   * Vendor in gopkg.in/go-jose/go-jose.v2 to v2.6.3
   * Vendor in github.com/go-jose/go-jose/v3 to v3.0.3
   * Vendor in github.com/onsi/ginkgo/v2 to v2.18.0
   * Vendor in  google.golang.org/protobuf to v1.33.0
   * Vendor in github.com/opencontainers/runtime-spec to v1.2.0
   * Vendor in golang.org/x/exp to v0.0.0-20240416160154-fe59bbe5cc7f
   * Vendor in golang.org/x/net to v0.25.0

* Tests
   * tests: skip_if_no_unshare(): check for --setuid by @edsantiago in  [#5360](https://github.com/containers/buildah/pull/5360)
   * pr-should-include-tests: use GitHub label, not commit text by @edsantiago in  [#5374](https://github.com/containers/buildah/pull/5374)
   * tests: enable pasta tests by @Luap99 in  [#5381](https://github.com/containers/buildah/pull/5381)
   * Change RUN to comment in bud.bats by @TomSweeneyRedHat in  [#5415](https://github.com/containers/buildah/pull/5415)
   * Switch packit configuration to use epel-9-$arch instead of centos-stream+epel-next-9-$arch by @nalind in  [#5484](https://github.com/containers/buildah/pull/5484)
   * Integration tests: fixup use of _prefetch by @nalind in  [#5480](https://github.com/containers/buildah/pull/5480)
   * integration test: handle new labels in "bud and test --unsetlabel" by @nalind in  [#5487](https://github.com/containers/buildah/pull/5487)
   * Disable packit builds for centos-stream+epel-next-8 by @nalind in  [#5493](https://github.com/containers/buildah/pull/5493)
   * Integration tests: switch some base images by @nalind in  [#5499](https://github.com/containers/buildah/pull/5499)
   * CI VMs: bump to new versions with tmpfs /tmp by @edsantiago in  [#5470](https://github.com/containers/buildah/pull/5470)
   * Integration tests: fake up a replacement for nixery.dev/shell by @nalind in  [#5495](https://github.com/containers/buildah/pull/5495)
   * bud tests: fix breakage when vendoring into podman by @edsantiago in  [#5537](https://github.com/containers/buildah/pull/5537)

* Changes to the build infrastucture
   * Fix a build break on FreeBSD by @dfr in  [#5293](https://github.com/containers/buildah/pull/529)
   * [CI:DOCS] Stop rebasing renovate PRs automatically by @cevich in  [#5414](https://github.com/containers/buildah/pull/5414)
   * CI: bump VMs by @edsantiago in  [#5426](https://github.com/containers/buildah/pull/5426
   * [skip-ci] Fix issue/pr lock workflow by @cevich in  [#5466](https://github.com/containers/buildah/pull/546)
   * fix CentOS/RHEL build - no BATS there by @jnovy in  [#5528](https://github.com/containers/buildah/pull/5528)

* Plus a few minor fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin. We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions! If you haven't joined our community yet, don't wait any longer! Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
