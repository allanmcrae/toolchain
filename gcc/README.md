# GCC testsuite failures

The GCC testsuite currently shows 0 unexpected failures!

## Buildflag failures

There are still failures if we enable various build flags. It would be good to investigate these in more detail and ensure fixes are made (either here or upstream), or incompatibilities formally noted - details in the PKGBUILD.

## Unpatched testsuite issues

### Failures due to default SSP

I missed this one when patching PR70150...
https://gcc.gnu.org/bugzilla/show_bug.cgi?id=70150

Configuring GCC with --enable-default-ssp results in these failures:
```
FAIL: gcc.target/i386/mvc7.c scan-assembler foo.avx,
FAIL: gcc.target/i386/mvc7.c scan-assembler foo.default,
```

### Upstream regression #1
https://gcc.gnu.org/pipermail/gcc-patches/2021-November/583608.html
https://gcc.gnu.org/pipermail/gcc-patches/2021-November/584190.html
```
FAIL: gfortran.dg/vector_subscript_1.f90   -O1  execution test
FAIL: gfortran.dg/vector_subscript_1.f90   -O2  execution test
FAIL: gfortran.dg/vector_subscript_1.f90   -O3 -fomit-frame-pointer -funroll-loops -fpeel-loops -ftracer -finline-functions  execution test
FAIL: gfortran.dg/vector_subscript_1.f90   -O3 -g  execution test
FAIL: gfortran.dg/vector_subscript_1.f90   -Os  execution test
```

### Upstream regression #2
https://gcc.gnu.org/pipermail/gcc-patches/2021-December/586851.html
```
FAIL: gfortran.dg/unlimited_polymorphic_3.f03   -Os  execution test
```

### Upstream regression #3
Needs investigating
```
UNRESOLVED: gcc.target/i386/pr35513-8.c scan-assembler .long[ \\t]+0xb0008000
UNRESOLVED: gcc.target/i386/pr35513-8.c scan-assembler .section[ \\t]+.note.gnu.property,
```

## Patched testsuite issues

### Failures due to default PIE

https://gcc.gnu.org/bugzilla/show_bug.cgi?id=70150
TODO: submit patch to mailing list

Configuring GCC with --enable-default-pie results in these failures:

```
FAIL: gcc.target/i386/cet-sjlj-6a.c scan-assembler-times movq\\t.*buf\\\\+8 1
FAIL: gcc.target/i386/cet-sjlj-6a.c scan-assembler-times subq\\tbuf\\\\+8 1
FAIL: gcc.target/i386/cet-sjlj-6b.c scan-assembler-times movq\\t.*buf\\\\+16 1
FAIL: gcc.target/i386/cet-sjlj-6b.c scan-assembler-times subq\\tbuf\\\\+16 1
FAIL: gcc.target/i386/fentryname3.c scan-assembler 0x0f, 0x1f, 0x44, 0x00, 0x00
FAIL: gcc.target/i386/pr24414.c (test for excess errors)
FAIL: gcc.target/i386/pr93492-3.c scan-assembler \\t.cfi_startproc\\n\\tendbr(32|64)\\n.*.LPFE1:\\n\\tnop\\n1:\\tcall\\t__fentry__\\n\\tret\\n
FAIL: gcc.target/i386/pr93492-5.c scan-assembler \\t.cfi_startproc\\n.*.LPFE1:\\n\\tnop\\n1:\\tcall\\t__fentry__\\n\\tret\\n
FAIL: gcc.target/i386/pr98482-1.c scan-assembler movabsq\\t\\\\\$__fentry__, %r10\\n\\tcall\\t\\\\*%r10
```
