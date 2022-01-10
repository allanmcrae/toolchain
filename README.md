# Arch Linux Toolchain
(As packaged in a very opinionated way by Allan)

## Overview

These packages provide an alternative packaging of the toolchain (linux-api-headers, glibc, gcc and binutils) for Arch Linux.  See below for the key differences and potential problems. 

There are two options for using these PKGBUILDs.  You can clone the git repo directly and build them yourself.

The build order is:
* linux-api-headers
* glibc
* binutils
* gcc
* glibc
* binutils
* gcc

A helper script will be added in the future that will automate this build using Arch devtools. The build can take several hours depending on your hardware. Note there is no need to run the testsuite in the first pass of the build.

*Due to libiberty move (see below) there is some manual steps currently needed to install the packages into the build root.*

Alternatively, I will build these around once per month (or as necessary due to changes in Arch) and you can download the packages directly from my repository.  Add the following to your pacman.conf file, above all other repositories.

```
[toolchain]
Server = http://allanmcrae.com/toolchain
SigLevel = Required
```

These packages and repository databases are signed by a valid Arch Linux packager key.

## Major changes from Arch Linux packages

**No multilib**

You can still install lib32-glibc and lib32-gcc-libs to have support for running i686 programs, but you can not build multilib packages when using this toolchain.  Using the Arch devtools will allow you to build against the Arch toolchain.

**No separate gcc-libs package**

All the gcc packages are merged into one.  Splitting packages in makepkg was built around KDE which provides nice "make" targets for the subprojects.  GCC does not.  Look at the Arch PKGBUILD to see the hassle this causes.  The makepkg maintainer should provide a better way for package splitting...

**No support for Ada, D or ObjC**

No-one really needs those languages anyway.

**All sources from git branch**

This toolchain always builds from the head of the relevant git branch.  This means there is no (or at least very little) need for backporting patches.
Usually these builds will follow the latest release branch, but will occasionally use the development branch in the period leading up to release.

**No systemtap support**

The Arch glibc package pulls systemtap support by importing headers from systemtap into the glibc package.  I disagree with this approach.  Instead the systemtap package should be added as a dependency to glibc.  As I have no interest in systemtap, I will not provide a systemtap package just to build glibc with systemtap support.

**Libiberty provided by binutils**

The libiberty files were moved to the Arch gcc package about a decade ago on a temporary basis due to a bug in the binutils version.  This was never reverted. 

**No libcrypt compatibility library**

The legacy libcrypt.so.1 library is not provided by glibc.

## Known Issues

There is a dependency loop between binutils and gcc.  This due to merging gcc-libs into gcc.  This can cause pacman to output multiple warnings, though has no effect on installed packages.

Some of the [new buildflags](https://gitlab.archlinux.org/archlinux/rfcs/-/blob/master/rfcs/0003-buildflags.rst) cause (false positive) testsuite failures in gcc.  These are currently disabled completely, but should only be disabled during the check() phase.

## Potential Issues (that likely will not be fixed)

This is far less tested than the Arch packages, so may cause breakages.  Saying that, I have a decade of experience as toolchain maintainer for Arch Linux...

The packages are built against the Arch Linux stable repositoires. The rare soname bumps in the dependencies will require rebuilds that may not time perfectly with the Arch release.

The Linux kernel is tied to the version of GCC used to build it.  You may have a bad time if you need to build kernel modules.

No rebuilds for libtool or valgrind.  These packages get rebuilt in Arch with GCC and glibc updates respectively.  I will not do that unless really necessary.
