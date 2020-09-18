---
title: Buildah version 1.16.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.16.0 Release Announcement

We're pleased to announce the release of [Buildah](https://github.com/containers/buildah) [version 1.16.0](https://github.com/containers/buildah/releases/tag/v1.16.0) which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora 32 & 33 and RHEL 8.4.  This will also be shipped on CentOS, openSUSE and Ubuntu in the near future.  In addition, container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features the notable enhancements:  A number of changes made to the `bud` command in order to speed up build processing, a static build of Buidah is now available via nix,  environment variables can now be set in `containers.conf` and the `--jobs` option has been added to the `bud` command.

* A number of changes to the internal processing of the `bud` command have been made to speed up the processing of that command.  Some nice gains have been made and work continues on further improvements.
* The Nix package manager can now be run to create a static build of Buildah.
* Environment variables that will be common to all your container images can now be set in the containers.conf file.  See the containers.conf man page for more details.
* The `--jobs` option in the `bud` command now allows for multiple jobs to be run in parallel.  See the bud man page for more details.
<!--readmore -->

This release comprises changes made for v1.15.1 through v1.15.2 and v1.16.0.

## Release Changes

### Changes for v1.16.0

  * When a new layer is created in the build process, the time of the layer is no longer set to the current time if a timestamp is not provided.
  * The retry delay option values for retrying that were sent to the commit, pull and push commands are now honored.
  * The handling of seccomp is now done in the containers/common project.
  * The  `--timestamp` option has  been added to the `bud` and `commit` commands to allow the ‘create’ timestamp to be set to seconds since epoch, replacing the `--omit-timestamp` option.  See the respective man pages for more information.
  * The `--quiet` option should be more quiet.
  * Fix ownership of content copied using `COPY --from`, prior ownership information on files was being dropped.
  * Error handling was improved in the `run` command and a few messages were clarified.
  * A copier package is now used internally to rework the handling of caches during `ADD` and `COPY` operations.
  * When doing a `COPY` of an archive file, the destination file name was incorrectly being blanked out; this has been corrected.
  * The retry functions have been replaced by functions from the common/pkg/retry package.
  * A number of timestamp comparisons were being done with `==` and they have been converted to use `time.Time.Equal()` which is more accurate.
  * Fixed errors found in a Coverity scan.
  * Namespace handling options in the `bud`, `from` and `run` commands have been changed to match the same options in Podman.  In addition the `--network` option for `bud` now accepts the same values that the corresponding Podman command does.
  * A dependency on the xz package has been added to Buildah images that are built for [quay.io](https://quay.io/buildah).
  * Storage was not always shutdown as it should have been on error, which could lead to a leaked mount point.  This has been corrected.
  * The `COPY --from` command now works when an argument is given to it.
  * The version of Buildah used to build an image is now embedded in the  BuilderIdentityAnnotation within the image.
  * The /etc/host and /etc/resolv.conf files are no longer bound if network is not present in the container.
  * An unnecessary call to the function NewImage() has been removed from the build processing.
  * When processing multiple archives during a .dockerignore process, the processing would stop at the end of the first archive.  Now all archives are processed as they should be.
  * Fixed & added notes regarding problematic language in the codebase that were not inclusive.
  * Added a dependency on github.com/stretchr/testify/require.
  * The build processing now waits for stages that might not have even started yet instead of trying to continue and then failing.
  * Mounts under `/sys` were not always accessible to rootless users.  This has been corrected.
  * Environment variables can now be pre-declared in the containers.conf(5) file.
  * The right stage's image is now returned as the "final" image.
  * When build arguments and environment variables have duplicate names, the values are now deduplicated.  Build arguments override Default arguments and Environment variables set during the build process override both of those.
  * Made changes based on the project containers/libpod renaming itself to containers/podman.
  * A Containerfile to build the stable buildah image using Centos7 was added. 
  * A race condition has been created that would cause a failure if the container would exit before the runtime sent a signal.
  * Made changes to how Buildah handled the `/sys/fs/selinux` mountpoint so that it would be available to Podman.
  * The files needed to run VFS in the Buildah container images were added.
  * The value "readonly" can now be used as  an alias to "ro" in mount options.
  * The OS X specific `--consistency` mount option is now ignored.
  * When doing builds where one stage requires the result of an earlier stage, Buildah now waits for that first stage to complete before the dependent stage starts.
  * Resolved a possible race in map handling during build stage processing.
  * The Dockerfiles that build the Buildah container images now use a containers.conf file.
  * The `--jobs` option in the `bud` command now allows for multiple jobs to be run in parallel.  
  * Bump to v1.17.0-dev


### Overall Miscellaneous Changes  
* Documentation
  * Clarified the 'triples' format of the variable provided to the `bud` `--userns-uid-map` option.
  * The “Using Buildah with container registries” tutorial had some syntax errors corrected.
  * Added documentation for `.dockerignore` to the `add`, `bud`, and `copy` man pages.
  * The “Using Buildah to build images in a rootless OpenShift container” tutorial was added.
  * The commit manage page had some wording corrected and an example for `--rm` added.
  * Added the quay.io/containers/buildah image to the README.md in the contrib/buildahimage directory and made other changes to the document, including a known configuration issue with the fuse module on some systems.
  * Fixed markdown formatting issues in CHANGELOG.md.

* Vendored:
  * Vendor in github.com/containers/common v0.21.0
  * Vendor in giithub.com/containers/image/v5 v5.5.2
  * Vendor in github.com/containers/ocicrypt v1.0.3
  * Vendor in github.com/containers/storage v1.23.3
  * Vendor in github.com/onsi/ginkgo v1.14.0
  * Vendor in github.com/opencontainers/runc v1.0.0-rc92
  * Vendor in github.com/opencontainers/selinux v1.6.0
  * Vendor in github.com/openshift/imagebuilder v1.1.6
  * Vendor in go.etcd.io/bbolt v1.3.5
  * Vendor in golang.org/x/text v0.3.3

* Tests:
  * Added further `bud` regression tests.
  * Corrections were made to ‘.dockerignore’ bud integration tests.
  * Added more authentication tests to a local registry. 
  * BATS tests were made more robust to avoid intermittent CI test flakes.
  * Fixed a race hit during conformance tests.
  * Reworked the conformance testing from ginkgo to the default testing package.
  * Invoke the cmd/buildah tests with flags containing two dashes.
  * Added a test for `COPY` from a subdirectory to the conformance tests.
  * The conformance tests now ignore buildah.BuilderIdentityAnnotation labels when comparing images .
  * Increased the test timeout to 40 for the tests and to 45 minutes for the test job as recently added tests have run out of time when otherwise processing successfully.
  * A number of `run_buildah` commands within the test code were being sent to a unix pipe to validate the test run.  Most of these pipes have been replaced with a more appropriate call to `expect_output`.


* Changes to the build infrastructure
  * Added htpasswd in registry image calls due to new changes in the registry image.
  * 32bit builds now set the values for Inblock and Outblock appropriately.
  * Added a nix build to provide for static builds of Buildah.
  * Made a few adjustments to the initial nix work.
  * The version of Go that is used during CI testing is now logged for future reference.

* Plus a number of smaller fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
