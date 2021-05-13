---
title: Buildah version 1.12.0 Release Announcement
layout: default
author: tsweeney
categories: [releases]
tags: community, open source, buildah
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.12.0 Release Announcement

We're pleased to announce the release of Buildah version 1.12.0 which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora, RHEL 8, RHEL 7, CentOS, openSUSE and Ubuntu in the near future.  Also container images will be available at https://quay.io/repository/buildah/stable.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.

## Notable enhancements:
* A new `manifest` command.
* A new `--history` option for the `image` command.
* A new `--device` option has been added to the `bud` and `from` commands.
* Changes to the `--pull` option used by the `bud` and `from` commands.
* Buildah now uses a ‘Containerfile’ by default rather than a ‘Dockerfile’.
<!--readmore-->

This release comprises changes made for v1.11.1, v1.11.2, v1.11.3, v1.11.4, v1.11.5, v1.11.6 and v1.12.0.

## The major highlights of this release are:
* A `manifest` command has been added to allow a Docker manifest list or an OCI image index to be created, updated, inspected, pushed or removed.  See buildah-manifest (1) for more information.
* A `--history` option has been added to the `image` command to show the image name history.
* A `--device` option has been added to the `bud` and `from` commands.  It allows an additional device or devices to be added under a directory in the container.
* The `--pull` option for the `bud` and `from` commands now emulate the Docker functionality.  Also a `--pull-never` option has been added to both commands.  When used, only images in the local storage will be used.
* If the context directory has a file named `Containerfile`, the `bud` command will use that file instead of a file called `Dockerfile`.  If there is no `Containerfile` in the context directory, Buildah will use the `Dockerfile` if it is present.  The internal syntax of both files is the same.
* A number of errors that happened when using the COPY or ADD commands in a Dockerfile have been corrected.

## Release Changes

### Changes within v1.12.0

  * The `ADD` command in a Dockerfile can now use an http reference as the source location.
  * The internal storage opts is now overridden if --storage-driver  is provided.
  * Start using containers/common, this will allow for a single configuration file to be used by all container tools (Podman, Skopeo, Conmon, Buildah, etc.).
  * When the rootfs of a container is unmounted, it now uses MNT_DETACH to unmount everything below it.
  * When binding, less spurious warnings are shown for missing mountpoints.
  * A manifest error during `buildah commit` has been fixed.
  * Added the `--history` option to the `buildah images` command to display the image name history.
  * An error that arose when an equal sign was missing in the --from and --chown flags for COPY/ADD in  a Dockerfile has been corrected.
  * When a Dockerfile COPY uses a URL, it now returns an error as it should.
  * Fixed a .dockerignore exclude regression that caused the functionality to not work if no exclusions were specified.
  * When committing a Docker image, Buildah now always sets the ContainerID and ContainerConfig fields.
  * Added builder identity annotations to container images.
  * Enhanced error verbiage on unsafe symbolic link targets.
  * Added the OCIRuntime field to the `buildah info` output.
  * An appropriate error is returned if a command requires the use of an authfile and it does not exist.
  * When running `buildah bud --quiet` only the imageID is now displayed.
  * Fixed the `--pull` option for `bud` and `from` to emulate the functionality in Docker, also added the `--pull-never` option to both commands which will use only an image on the local storage or fail.
  * Configuration blobs for manifest lists are now handled appropriately.
  * A crash that could occur if an error was raised before the image’s name was established has been corrected.
  * Added a disableFips option to the secrets package.
  * When the Dockerfile had multiple `ADD` commands with a `tar.xz` file as the source, the cache would be reused even if the files in the tar file had changed.  This has been corrected.
  * The default authfile path is now the same as the other container tools which is set by the containers/image project.
  * A `manifest` command has been added to allow the manipulation and viewing of Docker manifest lists or OCI image indices
  * More than one device can be added under the directory using the `--device` option of the `bud` command.
  * The `bud` option now works if the context directory is a git repo.
  * Silence the "using cache" output in the `bud` command to ensure the `--quiet` option is fully quiet.
  * Better error handling has been added to the `commit` when an error is thrown from container/storage.
  * Fixed a crash when an invalid `COPY` --from flag was specified in  a Dockerfile.
  * Fixed an error with --build-args handling when the Dockerfile `COPY` or `ADD` commands used the specified variable.
  * Added support for retrieving context from stdin "-" to the `bud` command.
  * The version of cgroup used by the system is now shown in the `buildah info` command.
  * The build 'STEP' output line now prints to stdout, not stderr.
  * The ‘bud` command now uses a file called ‘Containerfile` by default.
  * Added a `--device` option to the `bud` and `from` commands to allow additional devices to be added.  Reference the man pages for each command for more information.
  * Add support for /run/.containerenv which allows a container process to verify if they are running in a container or not.
  * Image names displayed in the `image` command are truncated to 32 characters.
  * File and directory mount permissions are now set after taking umask into consideration.
  * TMPDIR is now set to /var/tmp by default.
  * Allow mounts.conf entries entries can be simplified if the source and destination are the same path.
  * Labels and annotations now work appropriately for 1-line Dockerfiles.
  * Bump to v1.12.0-dev.

### Overall Miscellaneous Changes  
* Ran buildah through codespell.
* Enabled interfacer linter and fixed lints.

* Documentation changes:
  * Add an OWNERS File to the Buildah GitHub repository.
  * Updated install.md concerning golang dependency and mention goproxy.
  * Fixed the troubleshooting redirect instructions.
  * Add clarification to the Tutorial for new users.
  * Touched up the commit man page image parameter.

* Vendored:
  * Bump github.com/cyphar/filepath-securejoin from 0.2.1 to 0.2.2.
  * Bump github.com/containers/image to v5.0.0.
  * Bump to github.com/containers/storage v.1.15.3.
  * Bump github.com/etcd-io/bbolt from 1.3.2 to 1.3.3.
  * Bump github.com/fsouza/go-dockerclient from 1.4.4 to 1.5.0.
  * Bump github.com/mattn/go-shellwords from 1.0.5 to 1.0.6.
  * Bump github.com/onsi/ginkgo from 1.8.0 to 1.10.3.
  * Bump github.com/onsi/gomega from 1.5.0 to 1.7.1.
  * Bump github.com/opencontainers/selinux from 1.2.2 to 1.3.0.
  * Bump github.com/openshift/imagebuilder from 1.1.0 to 1.1.1.
  * Bump github.com/seccomp/libseccomp-golang from 0.9.0 to 0.9.1.
  * Bump github.com/spf13/cobra from 0.0.3 to 0.0.5.
  * Bump github.com/spf13/pflag from 1.0.3 to 1.0.5.
  * Bump github.com/stretchr/testify from 1.3.0 to 1.4.0.

* Tests:
  * Tests: Add inspect test check steps.
  * Tests: Add container name and id check in containers test steps.
  * Tests: Get permission in add test.
  * Tests: Add a test for tag by id.
  * Tests: Add test cases for push test.
  * Tests: Add image digest test.
  * Tests: Add some buildah from tests.
  * Tests: Add two commit test.
  * Tests: Add buildah bud with --quiet test.
  * Tests: Add two tests for buildah add.
  * Update tests for cgroup v2: tweak or skip tests.
  * Prepwork: new 'skip' helpers for tests.
  * Update bud.bats test archive test.
  * Add test for caching based on content digest.
  * Fix another broken test: copy-url-mtime.
  * Actual bug fix for 'add' test: fix the expected mode.
  * BATS tests - lots of mostly minor cleanup.
  * Fix travis-ci on forks.
  * Bumped the Fedora version from 28 to 30 in the test system.
  * In the test scripts, replace --debug=false with --log-level=error.

* Plus a number of smaller fixes.

## Try it Out.

If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/main/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
