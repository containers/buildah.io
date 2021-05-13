---
title: Buildah version 1.15.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]

tags: community, open source, buildah, hpc
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.15.0 Release Announcement

We're pleased to announce the release of Buildah version 1.15.0 which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora, RHEL 8, CentOS, openSUSE and Ubuntu in the near future.  Also container images will be available at https://quay.io/repository/buildah/stable and https://quay.io/repository/containers/buildah.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  This release features new options for the `push`, `pull`, `bud`, `from` and `commit` commands for encryption and decryption, in addition the `pull`, `from`, `commit` and `push` commands will now retry on most failures, the `buildah login` command is now usable as a rootless user, and many bug fixes.  Notable enhancements:  

* There are three new options: `--encryption-key`, `--encrypt-layer`, and `--decryption-key` that are usable from the `push`, `pull`, `bud`, `from` and `commit` commands as appropriate.  Please reference the man page for each of these commands for more details.
* The `pull`, `from`, `commit`, and `push` commands will now automatically retry on most error conditions.  The default is to retry 3 times at 2 second intervals.
* Rootless users were not able to login into a registry using `buildah login`. This has been corrected.
<!--readmore -->

This release comprises changes made for v1.14.1 through v1.14.8 and v1.15.0.

## Release Changes

### Changes for v1.15.0

 * Removed a dependency on an openshift struct which reduced the executable size by 25%.
 * Warnings are now issued when an ARG variable does not have a value set.
 * The encryption-key, encrypt-layer and decryption-keys have been created for the push, pull, bud, from and commit commands. 
 * Fixed and issue with the handling of `docker:` in Docker Official images.
 * Add preliminary profiling support to the CLI for memory and CPU.  These options are not currently supported.
 * A symlink issue when .dockerignore was evaluated has been addressed.
 * The handling of a build stage has been adjusted to not use a stage for further building until the stage has fully completed.
 * Fix permissions on containers.conf so that it can be read by a rootless container.
 * The exit code from failed containers in a build process are now showing the correct error.
 * The c/common/pkg/auth is now used with the login/logout commands.
 * Removed an invalid warning about systemd inside of container.
 * Internal error handling conventions were changed to show errors more appropriately.
 * Arguments are only added to the history when they are in scope for the build making process.
 * Fixed fips-mode check for RHEL8 boxes.
 * Fixed a potential CVE in tarfile with symlinks (Addresses CVE-2020-10696).
 * Fixed issues with .dockerignore handling of globs and ! commands.
 * Fixed compilation errors on non linux platforms.
 * Volume uid and gid values are now retained through the build process.
 * If a file was not pollable during the run process, it is not repolled unless there's a chance of a following poll working based on the returned errors.  This improves the speed of RUN.  
 * The local runtime image is now searched for per values in containers.conf.
 * The ownership of the working directory is now set appropriately so it can be written to.
 * Replace unix.* calls with syscall.* calls within Buildah to allow vendoring into libpod/Podman which needs to run in Linux and non-Linux environments.
 * A remote manifest can now be retrieved by specifying its name.
 * Adjustments were made to manifest handling which makes it easier to determine when to convert v2s1 images to v2s2 images.
 * The order in which elements are added to $PATH has been changed to prioritize those passed from containers.conf, those from the base image, and then those pass from the API.
 * OCI images don't always have a creation date set, the code now checks that it is before dereferencing it.
 * The commit id from a build is been made more clear and some "noisy" output from the build process has been removed.
 * When copying a file above the context directory during a build, a less confusing error message is now provided.
 * The pull/from/commit/push commands now retry on most failures, retrying 3 times every 2 seconds by default.
 * Buildah now makes use of the containers.conf configuration file.
 * Non-root users are now able to log into a registry using `buildah login`. 
 * Bump to v1.15.0-dev


### Overall Miscellaneous Changes  
* Documentation
  * Added a Code of Conduct.
  * Added a Security Policy.
  * Added a Pull Request Template.
  * Fixed the lighttpd example.
  * Updated the unshare man page to fix script example.
  * Included installation steps for CentOS 8.
  * Included installation steps for CentOS7 and forks.
  * Adjusted Ubuntu install information to also work on Pop!_OS.
  * Added CVE-2020-10696 notation to pertinent entries in CHANGELOG.md and changelog.txt.
  * Updated the installation steps for Amazon Linux 2.
  * Fixed formattig issues in the build instructions and made some minor modifications.

* Vendored:
  * Vendor in go.etcd.io/bbolt v1.3.4
  * Vendor in github.com/containers/common v0.13.1
  * Vendor in github.com/containers/image/v5 v5.4.4
  * Vendor in github.com/containers/storage v1.20.2
  * Vendor in github.com/fsouza/go-dockerclient v1.6.5
  * Vendor in github.com/mattn/go-shellwords v1.0.10
  * Vendor in github.com/onsi/ginkgo v1.12.3
  * Vendor in github.com/opencontainers/runc v1.0.0-rc90
  * Vendor in github.com/opencontainers/selinux v1.5.2
  * Vendor in github.com/openshift/imagebuilder v1.1.5
  * Vendor in github.com/opencontainers/go-digest v1.0.0
  * Vendor in gitthub.com/seccomp/containers-golang v0.5.0
  * Vendor in github.com/stretchr/testify v1.6.1
  * Vendor in github.com/sirupsen/logrus v1.6.0
  * Vendor in github.com/spf13/cobra v0.0.7

* Tests:
  * Updated exit code for tests.
  * Don't force tests to use runc.
  * Update gitignore to exclude test Dockerfiles.
  * dockerignore tests : remove symlinks, rework.
  * Fix bud-build-arg-cache test.
  * Digest test : make more robust.
  * Add comment for RUN command in volume ownership test.
  * Run stat command directly for volume ownership test.
  * Add tests for volume ownership.
  * Skip overlay test w/ vfs driver.
  * Use alpine, not centos, for various tests.
  * bud.bats - cleanup, refactoring.
  * BATS : in teardown, umount stale mounts.
  * Show validation command-line in tests.

* Changes to the build infrastructure
  * Bors: Fix no. req. github reviews.
  * Bors: Workaround ineffective required statuses.
  * Bors: Enable app + Disable Travis.
  * Bors-ng: Add documentation and status-icon.
  * Cirrus: Temporarily disable Ubuntu 19 testing.
  * Cirrus: Fixes from review feedback.
  * Cirrus: Use pre-installed VM packages + F32.
  * Cirrus: Re-enable all distro versions.
  * Cirrus: Update to F31 + Use cache images.
  * Cirrus+Bors: Simplify temp branch skipping.
  * Cirrus: Disable F29 testing.
  * Cirrus: Add jq package.
  * Cirrus: Fix lint + validation using wrong epoch.
  * Cirrus: Add standardized log-collection.
  * Cirrus: Improve automated lint + validation.
  * Cirrus: Fixes from review feedback.
  * Cirrus: Temporarily ignore VM testing failures.
  * Cirrus: Migrate off papr + implement VM testing.
  * Cirrus: Update packages + fixes for get_ci_vm.sh.
  * Allow passing options to golangci-lint.
  * Stop using fedorproject registry.
  * golangci-lint: Disable gosimple.
  * Lower number of golangci-lint threads.
  * Make vendor: run `tidy` after `vendor`.
  * Added .swp files to .gitignore.

* Plus a number of smaller fixes.

## Try it Out.
 
If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/main/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
