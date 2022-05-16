# Alternative Arch Linux Toolchain
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

A helper script is available that automates this build using Arch devtools. The build can take several hours depending on your hardware. Note there is no need to run the testsuite in the first pass of the build.

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

**Minimum kernel version of 5.10**

The Arch glibc package supports kernel version >= 4.4.  This means glibc is unable to use some optimisatons, but does allow Arch to run in more places. I will bump this two the second last LTS kernel version.

**No support for Ada, D or ObjC**

No-one really needs those languages anyway.

**All sources from git branch**

This toolchain always builds from the head of the relevant git branch.  This means there is no (or at least very little) need for backporting patches.
Usually these builds will follow the latest release branch, but will occasionally use the development branch in the period leading up to release.

**No systemtap support**

The Arch glibc package pulls systemtap support by importing headers from systemtap into the glibc package.  I disagree with this approach.  Instead the systemtap package should be added as a dependency to glibc.  As I have no interest in systemtap, I will not provide a systemtap package just to build glibc with systemtap support.

**No debuginfod supoprt**

The glibc package is now completely stripped following the Arch package.  Arch provides needed symbols for valgrind (and gdb?) to run via debuginfod.  You can install the need glibc-debug package directly from this repo.

## Known Issues

Some of the [new buildflags](https://gitlab.archlinux.org/archlinux/rfcs/-/blob/master/rfcs/0003-buildflags.rst) cause (false positive) testsuite failures in gcc.  These are currently disabled completely, but should only be disabled during the check() phase.

## Potential Issues (that likely will not be fixed)

This is far less tested than the Arch packages, so may cause breakages.  Saying that, I have a decade of experience as toolchain maintainer for Arch Linux...

The packages are built against the Arch Linux stable repositoires. The rare soname bumps in the dependencies will require rebuilds that may not time perfectly with the Arch release.

The Linux kernel is tied to the version of GCC used to build it.  You may have a bad time if you need to build kernel modules.

No rebuilds for libtool or valgrind.  These packages get rebuilt in Arch with GCC and glibc updates respectively.  I will not do that unless really necessary.
