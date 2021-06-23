---
title: Buildah version 1.20.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc, opensource, containers, images, image
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.20.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.20.0](https://github.com/containers/buildah/releases/tag/v1.20.0), which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 32, 33 & 34, and RHEL 8.5.  Buildah will also be shipped on CentOS, OpenSUSE, and Ubuntu soon.  In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features these notable enhancements: 

  * A number of packages and dead code have been removed from Buildah to shrink the size of its executable.
    * This included moving the internal structure definitions in Buildah to the ‘define’ subdirectory, so tools like Podman that vendor in Buildah could be streamlined.
  * Buildah’s copy processing has been changed to speed up the processing and better support rootless users.
  * Multi-arch container images are now built automatically and are available for Buildah on [quay.io](quay.io/containers/buildah)
  * The `buildah add` and `buildah copy` commands have added the `--chmod`  option to set the destination permissions.
  * A few issues with the recently added `buildah manifest` command have been addressed.
  * A number of other bug fixes have been completed.

<!--readmore -->

This release comprises changes made for v1.19.0 through v1.20.0.

## Release Changes

### Changes for v1.20.0
  * Multi-arch Buildah container images are now provided on [quay.io](quay.io/containers/buildah).
  * Use a faster way to check the container image for a version tag existence during multi-arch build of Buildah images on quay.io.
  * Look for a `Containerfile` file if the user specifies a directory with the `--file`/`-f` option in the `bud` command.
  * Added a number of changes to Bulidah’s copy logic to gain speed improvements and allow more robust functionality for rootless users.
  * Changes were made to allow the different kinds of pull to work with Podman’s REST API.
  * An image would not be pulled when pulling a specific architecture and the same image with a different architecture was already present.
  * Permissions set on the destination directory of a container using overlayfs were not always set.  This has been corrected.
  * A number of unused packages were removed to shrink the size of the Buildah executable.
  * Added a colon to the `buildah images <image_name>` error message to differentiate the error message from the error-inducing image name.
  * The add/copy man pages now have `--chmod` examples.
  * The `buildah login` and `buildah logout` commands entered user namespace and did not need to.  This has been corrected.
  * Bash completions for the `chmod` and `chown` options have been corrected.
  * If an image was built with an older version of Buildah, the Buildah version label in the image is now being updated when a newer version of Buildah changes it.
  * The values of isolation strings: oci, chroot, and rootless, are now being handled appropriately.
  * Build stages with no instructions are no longer reaped.
  * The name of the base image is now stored in the comment of the image’s first layer.
  * The overlay file system has a new “volatile” mount option which reduces I/O by ignoring fsync and syncfs requests.  This has been enabled for Buildah containers.
  * A number of options in the `buildah config` command now support the `-`  value (single dash), which removes all values in the configuration for that option type.  Examples are `--label`, `--port`, and more.  See the [buildah config man page](https://github.com/containers/buildah/blob/main/docs/buildah-config.md) for details.
  * When building an image with the same build args, the cache was not used [Issue 2992](https://github.com/containers/buildah/issues/2992).  This has been corrected.
  * The `buildah add` and `buildah copy` commands have added the `--chmod`  option to set the destination permissions.
  * The `--iidfile` option now prefixes the imageId with a hash character compatible with Docker.
  * A few issues with the recently added `buildah manifest` command have been addressed.
  * Several changes were made to better handle the `--build-arg` option in the `buildah bud` command.
  * Local container images can now be looked up by digest.
  * The default OCI Runtime is now determined by the value in the containers.conf file.
  * If the destination of a volume mount does not exist, Buildah now creates the destination directory in the container rather than throwing an error.

 
### Overall Miscellaneous Changes  
* Documentation:
  * Fixed rootful typo in docs.
  * Added documentation and testing for `.containerignore`.
  * Clarified userns options in man pages.
  * Remove the duplicate arch and os from the `from` man page.
  * Fixed the tutorial for rootless mode.
  * Fixed the `--format` option documentation in the buildah push man page.
  * Add information about multi-arch images to the [buildahimage](https://github.com/containers/buildah/blob/main/contrib/buildahimage/README.md)Readme.
  * Added required devel packages to this [tutorial](https://github.com/containers/buildah/blob/main/docs/tutorials/04-include-in-your-build-tool.md).


* Vendored:
  * Vendor in containernetworking/cni to v0.8.1
  * Vendor in github.com/containers/common 0.35.3
  * Vendor in github.com/containers/image v5.10.5
  * Vendor in github.com/containers/ocicrypt 1.1.0
  * Vendor in github.com/containers/storage  v1.28.1
  * Vendor in github.com/fsouza/go-dockerclient 1.7.2
  * Vendor in github.com/hashicorp/go-multierror 1.1.1
  * Vendor in github.com/mattn/go-shellwords 1.0.11
  * Vendor in github.com/onsi/ginkgo 1.15.2
  * Vendor in github.com/onsi/gomega 1.11.0
  * Vendor in github.com/openshift/imagebuilder 1.2.0
  * Vendor in github.com/sirupsen/logrus 1.8.1
  * Vendor in github.com/spf13/cobra 1.1.3
  * Vendor in github.com/stretchr/testify  1.7.0
  * Vendor in golang.org/x/crypto v0.0.0-20201221181555-eec23a3978ad

* Tests:
  * Tests: prefetch: use Buildah, not Podman, for pulls.
  * COPY --chown: expand the conformance test.
  * Fix system test of 'containers -a'.
  * Update system test for 'from --cap-add/drop'.
  * Added further system tests.
  * Stop testing directory permissions with the latest Docker.
  * Remove a duplicate system test for 'buildah containers -a'.
  * Fix the "overlay source permissions" test in overlay.bats
  * Fix: Containerfiles - smaller set of userns u/gids.
  * A workaround for a RHEL gating test failure was added.


* Changes to the build infrastructure:
  * Update nix pin with `make nixpkgs`.
  * Added a “stale” bot to remind maintainers when an issue has not been touched for over 30 days.
  * Cirrus: Temp. disable prior-fedora (F32) testing.
  * 'make validate': now require PRs to include tests.
  * Cirrus: Native OSX Build added.
  * Cirrus: Two minor cleanup items.

* Plus a number of smaller fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/main/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
