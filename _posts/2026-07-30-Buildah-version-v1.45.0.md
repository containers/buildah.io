---
title: Buildah version 1.45.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.45.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/podman-container-tools/buildah) [version 1.45.0](https://github.com/podman-container-tools/buildah/releases/tag/v1.45.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 45.  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon. In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/podman-container-tools/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable changes: 
<!--readmore -->
 *  A --no-follow-symlinks option to the `buildah add` command.
 *  A `--timestamp 0` option has been added to the `manifest push` command, which sets the timestamp on any tar entries to the specified time.
 *  Images built by `buildah build` without `--layers=true` will no longer add a layer with no contents to the output image if there were no changes to the working container's root filesystem during the build 
 *  The `buildah build` command now resolves references to stages using the last stage with a given name, rather than the first, when multiple stages use the same name
 *  CirrusCI closed in early June 2026.  A number of changes were made to the CI to account for that.
 *  The repository has moved from https://github.com/containers/buildah to https://github.com/podman-container-tools/buildah.  It is symlinked, but please note the new location.

This release comprises changes made for v1.45.0 and will be included in Podman v6.1.

## Release Changes
### Changes for v1.45.0
   * Add a --no-follow-symlinks option to `buildah add` to skip dereferencing the symlinks when copying by [@BenjaminSchubert](https://github.com/BenjaminSchubert) in [#6760](https://github.com/containers/buildah/pull/6760)
   * Add a `--timestamp 0` option to `manifest push`, which sets the timestamp on any tar entries to the specified time. by [@aeijdenberg](https://github.com/aeijdenberg) in [#6899](https://github.com/containers/buildah/pull/6899)
   * Buildah now honors containers.conf's seccomp_profile setting by [@jiwahn](https://github.com/jiwahn) in [#6908](https://github.com/containers/buildah/pull/6908)
   * Clean up TempDirForURL directories for --build-context and ADD git by [@Honny1](https://github.com/Honny1) in [#6881](https://github.com/containers/buildah/pull/6881)
   * The add and copy commands' --chmod argument now accepts symbolic notation, as well as the traditional numeric notation currently supported. Likewise, copier's GetOptions and PutOptions now have a Chmod option, which accepts numeric or symbolic notation, and if set overrides any ChmodDirs and ChmodFiles options by [@nickjwhite](https://github.com/nickjwhite) in [#6778](https://github.com/containers/buildah/pull/6778)
   * copier: add PutOptions.Timestamp for timestamp override by [@akca](https://github.com/akca) in [#6930](https://github.com/containers/buildah/pull/6930)
   * Images built by `buildah build` without `--layers=true` will no longer add a layer with no contents to the output image if there were no changes to the working container's root filesystem during the build by [@nalind](https://github.com/nalind) in [#6873](https://github.com/containers/buildah/pull/6873)
   * Reject explicit seccomp profiles when Buildah is not built with seccomp support by [@leonardomoreira00](https://github.com/leonardomoreira00) in [#6960](https://github.com/containers/buildah/pull/6960)
   * Fixed a build-cache bug where `RUN --mount` flags that omit `type=` (an implicit bind mount) were not checksummed for cache invalidation, causing builds to silently reuse a stale cached layer when only the mounted file's content changed by [@MayukhSobo](https://github.com/MayukhSobo) in [#6957](https://github.com/containers/buildah/pull/6957)
   * Restores the ability to explicitly specify "containers-storage:" when specifying base images for `buildah build` by [@nalind](https://github.com/nalind) in [#6982](https://github.com/containers/buildah/pull/6982)
   * Copier: add CreateDestPath option to PutOptions by [@ajoshua2004](https://github.com/ajoshua2004) in [#6976](https://github.com/containers/buildah/pull/6976)
   * Fixed chroot isolation RUN steps failing with "error setting supplemental groups list: operation not permitted" in user namespaces where setgroups is denied by [@ajoshua2004](https://github.com/ajoshua2004) in [#6961](https://github.com/containers/buildah/pull/6961)
   * fix: replace dead len > 2 guard with len != 2 in addSysctl by [@immanuwell](https://github.com/immanuwell) in [#6883](https://github.com/containers/buildah/pull/6883)
   * copier: add Symlink() for creating symlinks with inline target by [@ajoshua2004](https://github.com/ajoshua2004) in [#7001](https://github.com/containers/buildah/pull/7001)
   * `buildah build` now resolves references to stages using the last stage with a given name, rather than the first, when multiple stages use the same name by [@nalind](https://github.com/nalind) in [#6774](https://github.com/containers/buildah/pull/6774)  

* Documentation:
   * docs: fix typo dns-option by [@leonardomoreira00](https://github.com/leonardomoreira00) in [#6955](https://github.com/containers/buildah/pull/6955)
   * docs: update description for no-new-privileges option by [@leonardomoreira00](https://github.com/leonardomoreira00) in [#6952](https://github.com/containers/buildah/pull/6952)

* Vendored: 

  * Vendor github.com/containers/ocicrypt to v1.3.2
  * Vendor github.com/cyphar/filepath-securejoin to v0.7.0
  * Vendor github.com/docker/go-connections to v0.8.1
  * Vendor github.com/fsouza/go-dockerclient to v1.13.2
  * Vendor github.com/mattn/go-shellwords to v1.0.14
  * Vendor github.com/moby/buildkit to v0.31.2
  * Vendor github.com/moby/moby/client to v0.5.1
  * Vendor github.com/opencontainers/cgroups to v0.0.8
  * Vendor github.com/opencontainers/runc to v1.5.1
  * Vendor github.com/opencontainers/selinux to v1.15.1
  * Vendor github.com/pkg/sftp to v1.13.11
  * Vendor go.etcd.io/bbolt to v1.5.0
  * Vendor go.podman.io/common to v0.69.0
  * Vendor go.podman.io/image/v5 to v5.41.0
  * Vendor go.podman.io/storage to v1.64.0
  * Vendor google.golang.org/grpc to v1.83.0
  * Vendor golang.org/x/crypto to v0.54.0
  * Vendor golang.org/x/sync to v0.22.0
  * Vendor golang.org/x/sys to v0.47.0
  * Vendor golang.org/x/term to v0.45.0
  
* Tests:
   * Re-enable git ADD escape directory test by [@Honny1](https://github.com/Honny1) in [#6882](https://github.com/containers/buildah/pull/6882)
   * fix: typos in code comment by [@yaacov](https://github.com/yaacov) in [#6915](https://github.com/containers/buildah/pull/6915)
   * tests: fix "chroot with overlay root" flake by [@Luap99](https://github.com/Luap99) in [#6970](https://github.com/containers/buildah/pull/6970)

* Changes to the build infrastructure:
   * new gha ci with lima by [@timcoding1988](https://github.com/timcoding1988) in [#6884](https://github.com/containers/buildah/pull/6884)
   * ci: install cached Docker debs for debian conformance by [@timcoding1988](https://github.com/timcoding1988) in [#6889](https://github.com/containers/buildah/pull/6889)
   * CI image update and various CI improvements by [@Luap99](https://github.com/Luap99) in [#6911](https://github.com/containers/buildah/pull/6911)
   * Enable golangci-lint and codespell in CI and various CI and Makefile improvements by [@Luap99](https://github.com/Luap99) in [#6912](https://github.com/containers/buildah/pull/6912)
   * ci: also run on release branches by [@Luap99](https://github.com/Luap99) in [#6918](https://github.com/containers/buildah/pull/6918)
   * golangci-lint: enable nilnesserr, modernize and more govet checks by [@Luap99](https://github.com/Luap99) in [#6942](https://github.com/containers/buildah/pull/6942)
   * ci: make the automation release renovate managed by [@Luap99](https://github.com/Luap99) in [#6963](https://github.com/containers/buildah/pull/6963)
   * fix issue_pr_lock.yml workflow and do not run cronjobs at midnight by [@Luap99](https://github.com/Luap99) in [#6973](https://github.com/containers/buildah/pull/6973)
   * Add a workaround for using mount without privileges, re-enable rootless tests in CI by [@nalind](https://github.com/nalind) in [#6933](https://github.com/containers/buildah/pull/6933)
   * tests: add link to coreutils bug workaround by [@Luap99](https://github.com/Luap99) in [#6990](https://github.com/containers/buildah/pull/6990)

## New Contributors
  * [@yaacov](https://github.com/yaacov) made their first contribution in [#6915](https://github.com/containers/buildah/pull/6915)
  * [@jiwahn](https://github.com/jiwahn) made their first contribution in [#6908](https://github.com/containers/buildah/pull/6908
  * [@nickjwhite](https://github.com/nickjwhite)](https://github.com/nickjwhite)  made their first contribution in [#6778](https://github.com/containers/buildah/pull/6778)
  * [@leonardomoreira00](https://github.com/leonardomoreira00)  made their first contribution in [#6960](https://github.com/containers/buildah/pull/6960)
  * [@MayukhSobo](https://github.com/MayukhSobo)  made their first contribution in [#6957](https://github.com/containers/buildah/pull/6957)
  * [@immanuwell](https://github.com/immanuwell)  made their first contribution in [#6883](https://github.com/containers/buildah/pull/6883)



## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/podman-container-tools/buildah/blob/main/install.md) from one of the Linux repos or GitHub and give it a spin. We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions! If you haven't joined our community yet, don't wait any longer! Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity


