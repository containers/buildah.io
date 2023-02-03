---
title: Buildah version 1.29.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.29.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.29.0](https://github.com/containers/buildah/releases/tag/v1.29.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 36 and Fedora 37.  Buildah will also be shipped on CentOS, OpenSUSE, RHEL, and Ubuntu soon.  In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features notable enhancements: 
<!--readmore -->
   * The `prune` command has been added to clean intermediate images as well as the build and mount cache.
   * Added support for the `--group-add` option to the `from` and `build` commands. One useful feature of this, it to use the `–group-add keep-groups` option, which allows rootless users to take advantage of their group access to file and devices mounted into the build containers.
   * The `--cache-from` and `--cache-to` options for the `build` command now allow for multiple sources. This can be used to improve the speed of builds, especially in CI/CD environments.

This release comprises changes made for v1.28.1 and v1.28.2 and will be included in Podman v4.4.

## Release Changes

### Changes for v1.29.0
   * Fixed an issue with the `build` command when using the `--mount` option with the `RUN` command.  In some cases, the correct build stage was not being used ([#4522](https://github.com/containers/buildah/issues/4522)).
   * When the `--env` command line flag conflicts with an ENV instruction in a Containerfile, the Containerfile's value is now the one that is recorded in the output image.
   * Multiple `--label` command line flags now generate only one history entry in the output image.
   * The `--env` command line flag now generates a history entry in the output image.
   * Added support for the `--group-add` option to the `from` and `build` commands which assign additional groups to the primary user running within the container.
   * Fixed an error in the ignorefile handling when the file was a symlink.
   * Network setup errors have been clarified.
   *The Containerfile’s `RUN` command now allows relative mountpoints, in regards to the work directory, to be specified in the `--mount` option.
   * The `prune` command has been added to clean intermediate images as well as the build and mount cache.
   * The CleanCacheMount API can now be called outside of Buildah.
   * Multiple sources and destinations are now supported by the `--cache-from` and the `--cache-to` options of the `build` command.  See the `buildah-build (1)` man page for more details.
   * The Containerfile `RUN` commands `mount=type=cache` option now creates a separate cache parent on the host for each user.
   * Changes to the mount command were made to allow better operability on FreeBSD.
   * The `build` command now supports `--security-opt no-new-privileges` flag.
   * The base image honors userargs and heading args when built with the `build` `--all-platforms` option.
   * An error has been addressed that prevented the `--secret type=env` option from working when running the `build` command within a container.
   * Mult-stage builds now resolve the named image appropriately if a build arg is the same name.
   * When the `build` command used a `RUN --mount=type=bind` command to a previous stage, the contents were not accessible of the stage had been cached ([#4375](https://github.com/containers/buildah/issues/4375)).  This has been fixed. 
   * An issue with the `build` `---cache-from` not working properly with the `ARG` command has been corrected ([#4315](https://github.com/containers/buildah/issues/4315)).
   * Locking mechanisms used for cacheing were simplified within the code and an issue was locks with multiple mounts was fixed..
   * Simplify the interface of GetCacheMount and getCacheMount.
   * When using the `--mount=type=secret` option for the Containerfile `RUN` command, relative paths from the configured work directory can now be specified. 
   * When cached volumes were mounted with locking enabled, the `RUN` clause could hang ([#4342](https://github.com/containers/buildah/issues/4342)).  This has been corrected.
   * A Warning message is no longer shown for an argument that was not used during the build process ([#4303](https://github.com/containers/buildah/issues/4303)).
   * The Containerfiles used to build the variety of Buildah container images on quay.io has been consolidated into one file.
   * Bump to v1.28.1-dev.

### Overall Miscellaneous Changes  
* Documentation:
   * Fixed two diversity issues in a tutorial.
   * An unnecessary sudo in the main README.md's example on lighttpd was removed.
   * The `build --squash` option has been clarified.
   * Documentation was added for the `buildah build --pull=missing` option.
   * Fixed the installation instructions for Gentoo Linux.
   * Fixed the man pages to match the options the various commands have.

* Vendored:
   * Vendor in github.com/containerd/containerd 1.6.15
   * Vendor in github.com/containers/common 0.51.0
   * Vendor in github.com/containers/image 5.24.0
   * Vendor in github.com/containers/ocicrypt 1.1.6
   * Vendor in github.com/containers/storage 1.45.3
   * Vendor in github.com/docker/docker 20.10.23
   * Vendor in github.com/fsouza/go-dockerclient 1.9.3
   * Vendor in github.com/onsi/gomega 1.26.0
   * Vendor in github.com/spf13/cobra 1.6.0
   * Vendor in golang.org/x/crypto 0.4.0
   * Vendor in golang.org/x/sys 0.3.0
   * Vendor in golang.org/x/term 0.3.0

* Tests:
   * Flake 3710 has been closed. Reenable the test.
   * Tests: improve build-with-network-test.
   * Fix bud-multiple-platform-with-base-as-default-arg flake.
   * Tests: change the runtime-flag test for crun   * system tests: remove unhelpful assertions.
   * Test: fix preserve rootfs with --mount for podman-remote.
   * Test: fix prune logic for cache-from after adding content summary.
   * Test: cleaning cache must not clean lockfiles.
   * Update tests for error message changes.
   * Test: retrofit 'bud with undefined build arg directory'.
   * Test: bud.bats refactoring: $TEST_SCRATCH_DIR, part 2 of 2.
   * Test: bud.bats refactoring: $TEST_SCRATCH_DIR, part 1 of 2.
   * Userns: add arbitrary steps/stage to --userns=auto test.
   * System test cleanup: document, clarify, fix.
   * Test: removing unneeded/expensive COPY.
   * Removed a number of  unnecessary, hence misleading, `rmi` commands in the tests.
   * Test: warning behaviour for unset/set TARGETOS,TARGETARCH,TARGETPLATFORM.
   * Define and use a safe, reliable test image.
   * A locking issue regarding ssh was corrected in the test suites.

* Changes to the build infrastructure:
   * Cirrus: Update VM Images.
   * Fixed a multi-arch manifest-list build timeouts.
   * Update to F37 CI VM Images, re-enable prior-fedora.
   * Cirrus: Migrate OSX task to M1.
   * GHA: Reuse both cirrus rerun and check workflows.
   * GHA: Simplify Cirrus-Cron check slightly.
   * Makefile: Fix install on FreeBSD.
   * [CI:BUILD] copr: buildah rpm should depend on containers-common-extra.
   * Cirrus CI add flavor parameter.
   * Makefile: Use $(MAKE) to start sub-makes in install.tools.
   * pr-should-include-tests: allow specfile, golangci.

* Plus several minor fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
