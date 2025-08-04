---
title: Buildah version 1.41.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.41.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.41.0](https://github.com/containers/buildah/releases/tag/v1.41.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 41 and Fedora 42.  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon. In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable changes: 
<!--readmore -->
 * A number of changes have been made to allow for “reproducible builds”, which, in specific scenarios, should reduce the pull time of images.
 * The `--inherit-annotations`, `--source-date-epoch`, `--rewrite-timestamp`, and `--unsetannotation` commands have been added to the `build` command.  See the `build` man page for more details.
 * The `--link` option on the `COPY` and `ADD` commands in a Containerfile now fully supports layered build caching.

This release comprises changes made for v1.41.0 and will be included in Podman v5.6.

## Release Changes
### Changes for v1.41.0
   * Filter image only when necessary, which reduces overhead when creating images by [@hanwen-flow](https://github.com/hanwen-flow) in [#6141](https://github.com/containers/buildah/pull/6141)
   * Support label_users in buildah from containers.conf by [@rhatdan](https://github.com/rhatdan) in [#6161](https://github.com/containers/buildah/pull/6161)
   * Fix typo in comment by [@brawer](https://github.com/brawer) in [#6167](https://github.com/containers/buildah/pull/6167)
   * Refactor NewImageSource to add a manifest type abstraction by [@aaronlehmann](https://github.com/aaronlehmann) in [#5743](https://github.com/containers/buildah/pull/5743)
   *When using --layers buildah will select most recent layer in case of conflict by [@flouthoc](https://github.com/flouthoc) in [#6171](https://github.com/containers/buildah/pull/6171)
   * The `buildah build`'s "--output" option can now be specified multiple times by [@nalind](https://github.com/nalind) in [#6177](https://github.com/containers/buildah/pull/6177)
   * The `buildah add` command now offers a "--timestamp" option by [@nalind](https://github.com/nalind) in [#6178](https://github.com/containers/buildah/pull/6178)
   * Fixed the link to the Maintainers file by [@JayKayy](https://github.com/JayKayy) in [#6187](https://github.com/containers/buildah/pull/6187)
   * The `buildah build --add-host` option now automatically resolves host-gateway from a string by [@flouthoc](https://github.com/flouthoc) in [#6188](https://github.com/containers/buildah/pull/6188)
   * When the `--platform` option is not invoked, Buildah now uses the default platform.  When the `--platform` option is used, the platform information from the base image is now used  by [@nalind](https://github.com/nalind) in [#6190](https://github.com/containers/buildah/pull/6190)
   * Ensure extendedGlob returns paths in lexical order to achieve a reproducible build by [@Honny1](https://github.com/Honny1) in [#6169](https://github.com/containers/buildah/pull/6169)
   * The `buildah commit` command now recognizes `--source-date-epoch` and `--rewrite-timestamp` options, which affect the dates recorded in the new image's configuration and the timestamps on the contents of the new layer by [@nalind](https://github.com/nalind) in [#6189](https://github.com/containers/buildah/pull/6189)
   * The `buildah build` command now recognizes the `--source-date-epoch` and `--rewrite-timestamp` options, which affect the dates recorded in the new image's configuration and the timestamps on the contents of the new layers and content generated in response to the `--output` flag by [@nalind](https://github.com/nalind) in [#6208](https://github.com/containers/buildah/pull/6208)
   * Added support for the ‘--unsetannotation’ option, which allows users to prevent inheriting a specific annotation from base image in the build and config commands by [@flouthoc](https://github.com/flouthoc) in [#6195](https://github.com/containers/buildah/pull/6195)
   * The `buildah build`  sets a fixed hostname for RUN instructions when invoked with the `--timestamp` or `--source-date-epoch` options.
When building or committing images with the `--timestamp` or `--source-date-epoch` options, the hostname, domain name, and name-of-container-which-was-committed will be set to fixed values by [@nalind](https://github.com/nalind) in [#6211](https://github.com/containers/buildah/pull/6211)
   *The `buildah build` and `buildah commit` commands no longer sets/updates the `io.buildah.version` label by default when either the `--timestamp` or `--source-date-epoch` options are used by [@nalind](https://github.com/nalind) in [#6214](https://github.com/containers/buildah/pull/6214)
   * Support zstd compression is now working in image commit by [@aaronlehmann](https://github.com/aaronlehmann) in [#5452](https://github.com/containers/buildah/pull/5452)
   * Added support for the `--inherit-annotations` command to the `build` command which allows users to specify if they want to inherit annotations from base image or not by [@flouthoc](https://github.com/flouthoc) in [#6198](https://github.com/containers/buildah/pull/6198)
   * The `buildah build` command no longer leave traces of mount targets used for RUN instructions in built images by [@nalind](https://github.com/nalind) in [#6233](https://github.com/containers/buildah/pull/6233)
   * Images committed in OCI formats now default to including an "org.opencontainers.image.created" annotation by [@nalind](https://github.com/nalind) in [#6239](https://github.com/containers/buildah/pull/6239)
   * The BUILDTAG btrfs_noversion flag has been removed as it is no longer effective by [@rahilarious](https://github.com/rahilarious) in [#6267](https://github.com/containers/buildah/pull/6267)
   * The `--link` option on the `COPY` and `ADD` commands in a Containerfile now fully support layered build caching by [@2004joshua](https://github.com/2004joshua) in [#6240](https://github.com/containers/buildah/pull/6240)
   * The `build` command now makes sure that platform is considered correctly before using the potential image as cache candidate by [@flouthoc](https://github.com/flouthoc) in [#6269](https://github.com/containers/buildah/pull/6269)
      
* Documentation:
   * [CI:DOCS] update a couple of lists in the build man page by [@nalind](https://github.com/nalind) in [#6175](https://github.com/containers/buildah/pull/6175)
   * [CI:DOCS] Add CNCF roadmap, touchup other CNCF files by [@TomSweeneyRedHat](https://github.com/TomSweeneyRedHat) in [#6124](https://github.com/containers/buildah/pull/6124)
   * [CI:DOCS] README.md: add openssf passing badge by [@lsm5](https://github.com/lsm5) in [#6181](https://github.com/containers/buildah/pull/6181)
   * docs: add --setopt "*.countme=false" to dnf examples by [@nalind](https://github.com/nalind) in [#6215](https://github.com/containers/buildah/pull/6215)
   * Update Neil Smith's GitHub username in MAINTAINERS.md by [@actionmancan](https://github.com/actionmancan) in [#6248](https://github.com/containers/buildah/pull/6248)

* Vendored: 
   * Vendor in containers/automation_images to v20250422
   * Vendor in github.com/containers/common to v0.63.0
   * Vendor in github.com/containers/luksy digest to bc60f96
   * Vendor in github.com/containers/image/v5 to v5.36.0
   * Vendor in github.com/containers/storage to v1.59.0
   * Vendor in github.com/docker/docker to v28.3.2+incompatible
   * Vendor in github.com/fsouza/go-dockerclient to v1.12.1
   * Vendor in github.com/go-viper/mapstructure/v2 to v2.3.0
   * Vendor in github.com/moby/buildkit to v0.23.2
   * Vendor in github.com/openshift/imagebuilder to v1.2.16
   * Vendor in github.com/opencontainers/cgroups to v0.0.3
   * Vendor in github.com/opencontainers/runc to v1.3.0
   * Vendor in github.com/seccomp/libseccomp-golang to v0.11.0
   * Vendor in go.etcd.io/bbolt to v1.4.2
   * Vendor in golang.org/x/crypto to v0.40.0
   * Vendor in golang.org/x/sync to v0.16.0
   * Vendor in golang.org/x/term to v0.33.0
   
* Tests
   * test/serve: fix a descriptor leak, add preliminary directory support by [@nalind](https://github.com/nalind) in [#6146](https://github.com/containers/buildah/pull/6146)
   * commit-with-extra-files test: use $TEST_SCRATCH_DIR by [@nalind](https://github.com/nalind) in [#6231](https://github.com/containers/buildah/pull/6231)
   * Add conditional release-checking system test by [@cevich](https://github.com/cevich) in [#6243](https://github.com/containers/buildah/pull/6243)
   * Update "bud with --cpu-shares" test, and rename it by [@nalind](https://github.com/nalind) in [#6271](https://github.com/containers/buildah/pull/6271)
   * buildah: move passwd command to tests by [@flouthoc](https://github.com/flouthoc) in [#6264](https://github.com/containers/buildah/pull/6264)
   
* Changes to the build infrastructure
   * [skip-ci] Packit: Ignore ELN and CentOS Stream jobs by [@lsm5](https://github.com/lsm5) in [#6172](https://github.com/containers/buildah/pull/6172)
   * [skip-ci] Packit: set fedora-all after F40 EOL by [@lsm5](https://github.com/lsm5) in [#6170](https://github.com/containers/buildah/pull/6170)
   * Use Fedora 42 instead of 41 in that one conformance test by [@nalind](https://github.com/nalind) in [#6174](https://github.com/containers/buildah/pull/6174)
   * [skip-ci] Packit: Disable osh_diff_scan by [@lsm5](https://github.com/lsm5) in [#6164](https://github.com/containers/buildah/pull/6164)
   * remove static nix build by [@Luap99](https://github.com/Luap99) in [#6191](https://github.com/containers/buildah/pull/6191)   
   * Don't BuildRequires: ostree-devel by [@mtrmac](https://github.com/mtrmac) in [#6192](https://github.com/containers/buildah/pull/6192)
   * dynamically link sqlite by [@Luap99](https://github.com/Luap99) in [#6216](https://github.com/containers/buildah/pull/6216)
   * CI: give the rootless test user some supplemental groups by [@nalind](https://github.com/nalind) in [#6227](https://github.com/containers/buildah/pull/6227)
   * conformance: use mirrored frontend and base images by [@nalind](https://github.com/nalind) in [#6232](https://github.com/containers/buildah/pull/6232)
   * CI: ensure rootless groups aren't duplicates by [@nalind](https://github.com/nalind) in [#6228](https://github.com/containers/buildah/pull/6228)
   * Adjust a bud and run test as runc does not support keep-groups by [@ricardobranco777](https://github.com/ricardobranco777) in [#6226](https://github.com/containers/buildah/pull/6226)

### New Contributors
   * [@hanwen-flow](https://github.com/hanwen-flow) made their first contribution in [#6141](https://github.com/containers/buildah/pull/6141)
   * [@brawer](https://github.com/brawer) made their first contribution in [#6167](https://github.com/containers/buildah/pull/6167)
   * [@JayKayy](https://github.com/JayKayy) made theirfirst contribution in [#6187](https://github.com/containers/buildah/pull/6187)
   * [@ricardobranco777](https://github.com/ricardobranco777) made their first contribution in [#6226](https://github.com/containers/buildah/pull/6226)
   * [@actionmancan](https://github.com/actionmancan) made their first contribution in [#6248](https://github.com/containers/buildah/pull/6248)
   * [@pstoeckle](https://github.com/pstoeckle) made their first contribution in [#6252](https://github.com/containers/buildah/pull/6252)
   * [@2004joshua](https://github.com/2004joshua) made their first contribution in [#6240](https://github.com/containers/buildah/pull/6240)

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin. We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions! If you haven't joined our community yet, don't wait any longer! Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
