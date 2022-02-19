# GCC testsuite failures

## Buildflag failures

These are failures in the GCC testsuite if we do not remove various Arch default build flags. It would be good to investigate these in more detail and ensure fixes are made (either here or upstream), or incompatibilities formally noted.

### Failure with -fexceptions

These all look like -fexceptions causes the relevant testsuite to fail to build.

```
FAIL: c-c++-common/asan/pr59063-2.c   -O0  (test for excess errors)
UNRESOLVED: c-c++-common/asan/pr59063-2.c   -O0  compilation failed to produce executable
FAIL: c-c++-common/asan/pr59063-2.c   -O1  (test for excess errors)
UNRESOLVED: c-c++-common/asan/pr59063-2.c   -O1  compilation failed to produce executable
FAIL: c-c++-common/asan/pr59063-2.c   -O2  (test for excess errors)
UNRESOLVED: c-c++-common/asan/pr59063-2.c   -O2  compilation failed to produce executable
FAIL: c-c++-common/asan/pr59063-2.c   -O2 -flto -fno-use-linker-plugin -flto-partition=none  (test for excess errors)
UNRESOLVED: c-c++-common/asan/pr59063-2.c   -O2 -flto -fno-use-linker-plugin -flto-partition=none  compilation failed to produce executable
FAIL: c-c++-common/asan/pr59063-2.c   -O2 -flto -fuse-linker-plugin -fno-fat-lto-objects  (test for excess errors)
UNRESOLVED: c-c++-common/asan/pr59063-2.c   -O2 -flto -fuse-linker-plugin -fno-fat-lto-objects  compilation failed to produce executable
FAIL: c-c++-common/asan/pr59063-2.c   -O3 -g  (test for excess errors)
UNRESOLVED: c-c++-common/asan/pr59063-2.c   -O3 -g  compilation failed to produce executable
FAIL: c-c++-common/asan/pr59063-2.c   -Os  (test for excess errors)
UNRESOLVED: c-c++-common/asan/pr59063-2.c   -Os  compilation failed to produce executable
FAIL: libitm.c/alloc-1.c (test for excess errors)
UNRESOLVED: libitm.c/alloc-1.c compilation failed to produce executable
FAIL: libitm.c/cancel.c (test for excess errors)
UNRESOLVED: libitm.c/cancel.c compilation failed to produce executable
FAIL: libitm.c/clone-1.c (test for excess errors)
UNRESOLVED: libitm.c/clone-1.c compilation failed to produce executable
FAIL: libitm.c/dropref-2.c (test for excess errors)
UNRESOLVED: libitm.c/dropref-2.c compilation failed to produce executable
FAIL: libitm.c/dropref.c (test for excess errors)
UNRESOLVED: libitm.c/dropref.c compilation failed to produce executable
FAIL: libitm.c/memcpy-1.c (test for excess errors)
UNRESOLVED: libitm.c/memcpy-1.c compilation failed to produce executable
FAIL: libitm.c/memset-1.c (test for excess errors)
UNRESOLVED: libitm.c/memset-1.c compilation failed to produce executable
FAIL: libitm.c/notx.c (test for excess errors)
UNRESOLVED: libitm.c/notx.c compilation failed to produce executable
FAIL: libitm.c/priv-1.c (test for excess errors)
UNRESOLVED: libitm.c/priv-1.c compilation failed to produce executable
FAIL: libitm.c/reentrant.c (test for excess errors)
UNRESOLVED: libitm.c/reentrant.c compilation failed to produce executable
FAIL: libitm.c/simple-1.c (test for excess errors)
UNRESOLVED: libitm.c/simple-1.c compilation failed to produce executable
FAIL: libitm.c/simple-2.c (test for excess errors)
UNRESOLVED: libitm.c/simple-2.c compilation failed to produce executable
FAIL: libitm.c/stackundo.c (test for excess errors)
UNRESOLVED: libitm.c/stackundo.c compilation failed to produce executable
FAIL: libitm.c/txrelease.c (test for excess errors)
UNRESOLVED: libitm.c/txrelease.c compilation failed to produce executable
```

### Failure with -Wp,-D_FORTIFY_SOURCE=2/

```
FAIL: 17_intro/names.cc (test for excess errors)
FAIL: 18_support/exception_ptr/64241.cc (test for excess errors)
FAIL: 20_util/shared_ptr/creation/overwrite.cc (test for excess errors)
FAIL: 20_util/unique_ptr/creation/for_overwrite.cc (test for excess errors)
FAIL: 21_strings/basic_string/cons/char/8.cc (test for excess errors)
FAIL: 21_strings/basic_string/cons/wchar_t/8.cc (test for excess errors)
FAIL: 21_strings/basic_string/modifiers/64422.cc (test for excess errors)
FAIL: 21_strings/basic_string/operators/char/65630.cc (test for excess errors)
FAIL: 21_strings/basic_string/operators/wchar_t/65630.cc (test for excess errors)
FAIL: 23_containers/deque/allocator/default_init.cc (test for excess errors)
FAIL: 23_containers/forward_list/allocator/default_init.cc (test for excess errors)
FAIL: 23_containers/forward_list/operations/91620.cc (test for excess errors)
FAIL: 23_containers/list/allocator/default_init.cc (test for excess errors)
FAIL: 23_containers/list/operations/91620.cc (test for excess errors)
FAIL: 23_containers/map/allocator/default_init.cc (test for excess errors)
FAIL: 23_containers/set/allocator/default_init.cc (test for excess errors)
FAIL: 23_containers/unordered_map/allocator/default_init.cc (test for excess errors)
FAIL: 23_containers/unordered_set/allocator/default_init.cc (test for excess errors)
FAIL: 23_containers/vector/allocator/default_init.cc (test for excess errors)
FAIL: 23_containers/vector/bool/allocator/default_init.cc (test for excess errors)
FAIL: 26_numerics/complex/value_operations/1.cc (test for excess errors)
FAIL: 27_io/basic_fstream/cons/base.cc (test for excess errors)
FAIL: 27_io/basic_stringbuf/cons/char/default.cc (test for excess errors)
FAIL: 27_io/basic_stringbuf/cons/wchar_t/default.cc (test for excess errors)
FAIL: 28_regex/basic_regex/85098.cc (test for excess errors)
FAIL: 29_atomics/atomic/65913.cc (test for excess errors)
FAIL: experimental/filesystem/path/preferred_separator.cc (test for excess errors)
FAIL: experimental/names.cc (test for excess errors)
FAIL: ext/random/hypergeometric_distribution/pr60037.cc (test for excess errors)
```

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
https://gcc.gnu.org/pipermail/gcc-patches/2022-February/590571.html
```
FAIL: gcc.dg/deprecated.c  (test for warnings, line 28)
FAIL: gcc.dg/deprecated.c (test for excess errors)
```

### Upstream regression #4
https://gcc.gnu.org/pipermail/gcc-patches/2022-February/590443.html
```
FAIL: gcc.target/i386/auto-init-4.c scan-assembler-times long\\t-16843010 5
```

### Upstream regression #5
Needs investigating
```
FAIL: g++.dg/cpp23/consteval-if2.C  -std=gnu++20  (test for errors, line 80)
FAIL: g++.dg/cpp23/consteval-if2.C  -std=gnu++20  (test for errors, line 84)
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
