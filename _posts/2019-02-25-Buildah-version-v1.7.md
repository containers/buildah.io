---
title: Buildah version 1.7 Release Announcement
layout: default
author: tsweeney
categories: [releases]
tags: community, open source, buildah
---
![buildah logo](https://buildah.io/images/buildah.png)

# Buildah version 1.7 Release Announcement

We're pleased to announce the release of Buildah version 1.7 which is now available from GitHub for any Linux distro.  We are shipping this release on Fedora, RHEL 7, CentOS, openSUSE and Ubuntu in the near future.

The Buildah project has continued to grow over the past several weeks, welcoming several new contributors to the mix.  Updates were made to the performance of pulling and pushing images, an --add-history option has been added to several commands, the Cobra CLI is now being used and bug fixes.

<!--readmore-->
## The major highlights for this release are:

* If an image has multiple layers, the layers are pulled in parallel speeding up the time required to pull an image.  Reversely when pushed, the layers are pushed in parallel.
*  The `buildah bud` command now accepts a `--target` option which allows the build to only include the stages in the Dockerfile up to and including the specified stage.
* A new `--add-history` option has been added to the `buildah add`, `buildah config`, `buildah copy` and the `buildah run` commands.  This option allows you to add entries to a committed images history.  Please refer to the individual commands’ man page for more information.
* The CLI package used by Buildah is now spf13/Cobra which replaces urfave/cli.  The Buildah CLI should still function the same, if not please report an issue.  The CLI help messages that are seen with commands like `buildah pull --help` have had their format changed slightly due to this change.

## Release Changes
* Make "images --all" faster.
* Make sure buildah pull --all-tags only works with the Docker transport.
* Images pulled with the `buildah pull` command were not using the registries.conf file when looking up the registries, this has been corrected and emulates the `buildah bud` and `buildah from` commands.
* Do pushes and pulls of multi-layer container images in parallel.
* Errors encountered when running a mount command in rootless mode have been changed to make the errors more clear.
* A few changes were made to mitigate a few issues as discovered by CVE-2019-5736.
* Add --target to the `buildah bud` command.
* Fixed a few issues with informational commands like `buildah version` and `buildah info` when run in rootless mode.
* A few internal changes were made to rootless mode functionality to allow it to work more efficiently.
* Replace urfave/cli with spf13/Cobra.
* Add Quiet to the PullOptions and PushOptions in the internal API.
* The `--omit-timestamp` option has been added to the `buildah commit` command to allow images to have the same output if the commit command is run multiple times.  See `buildah commit(1)` for more details.
* A new `--add-history` option has been added to the `buildah add`, `buildah config`, `buildah copy` and the `buildah run` commands.  Please refer to their man pages for more details.
* When creating a container, the passed in path was not always created as it should have been.  This has been corrected.
* Changes related to Dockerfile handling:
  * Two line Dockerfiles were not being processed appropriately, this has been corrected.
  * Added support for `ADD --chown`.
* Documentation changes:
  * The mount man page has had further instructions added on how to mount in rootless mode.
  * CLI help descriptions and usage have been changed to be a bit more consistent.
  * The healthcheck start-period documentation has been updated.
  *  The example for setting multiple environment variables in the ` buildah config` man page has been fixed.
* Tests: A number of corrections and creations were added.
* Plus a number of smaller fixes.

## Try it Out.

If you haven’t yet, [install Buildah](https://github.com/containers/buildah/blob/master/install.md) from one of the Linux repos or GitHub and give it a spin.  We’re betting you'll find it’s an easy and quick way to build containers in your environment without a daemon being involved!

For those of you who contributed to this release, thank you very much for your contributions!  If you haven't joined our community yet, don't wait any longer!  Come join us on GitHub, where Open Source communities live.

## Buildah == Simplicity
