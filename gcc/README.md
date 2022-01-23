# GCC testsuite failures

The GCC testsuite currently shows 44 failures.  It would be good to investigate these in more detail and ensure fixes are made (either here or upstream), or incompatibilities formally noted.

## Analyzer failures due to glibc-2.34+ incompatibility

https://gcc.gnu.org/bugzilla/show_bug.cgi?id=101081

```
FAIL: gcc.dg/analyzer/analyzer-verbosity-2a.c (test for excess errors)
FAIL: gcc.dg/analyzer/analyzer-verbosity-3a.c (test for excess errors)
FAIL: gcc.dg/analyzer/edges-1.c (test for excess errors)
FAIL: gcc.dg/analyzer/file-1.c (test for excess errors)
FAIL: gcc.dg/analyzer/file-2.c (test for excess errors)
FAIL: gcc.dg/analyzer/file-paths-1.c (test for excess errors)
FAIL: gcc.dg/analyzer/file-pr58237.c (test for excess errors)
FAIL: gcc.dg/analyzer/pr99716-1.c (test for excess errors)
```

## Failures due to default SSP

Configuring GCC with --enable-default-ssp results in these failures:

```
FAIL: gcc.dg/asan/use-after-scope-4.c   -O0  execution test
FAIL: gcc.dg/stack-usage-1.c scan-stack-usage foo\\t(256|264)\\tstatic
FAIL: gcc.dg/superblock.c scan-rtl-dump-times sched2 "ADVANCING TO" 2
FAIL: gcc.target/i386/avx-vzeroupper-17.c scan-assembler-times avx_vzeroupper 1
FAIL: gcc.target/i386/cleanup-1.c execution test
FAIL: gcc.target/i386/cleanup-2.c execution test
FAIL: gcc.target/i386/interrupt-redzone-1.c scan-assembler-not \\tcld
FAIL: gcc.target/i386/interrupt-redzone-2.c scan-assembler-not \\tcld
FAIL: gcc.target/i386/pr79793-1.c scan-assembler-times add[lq][\\t ]*\\\\\$400,[\\t ]*%[re]sp 1
FAIL: gcc.target/i386/pr79793-1.c scan-assembler-times fxsave64[\\t ]*-120\\\\(%[re]sp\\\\) 1
FAIL: gcc.target/i386/pr79793-1.c scan-assembler-times sub[lq][\\t ]*\\\\\$400,[\\t ]*%[re]sp 1
FAIL: gcc.target/i386/pr79793-2.c scan-assembler-times add[lq][\\t ]*\\\\\$400,[\\t ]*%[re]sp 1
FAIL: gcc.target/i386/pr79793-2.c scan-assembler-times fxsave64[\\t ]*-120\\\\(%[re]sp\\\\) 1
FAIL: gcc.target/i386/pr79793-2.c scan-assembler-times sub[lq][\\t ]*\\\\\$392,[\\t ]*%[re]sp 1
FAIL: gcc.target/i386/shrink_wrap_1.c scan-rtl-dump pro_and_epilogue "Performing shrink-wrapping"
FAIL: gcc.target/i386/stack-check-11.c scan-assembler-times or[ql] 3
FAIL: gcc.target/i386/stack-check-11.c scan-assembler-times sub[ql] 4
FAIL: gcc.target/i386/stack-check-18.c scan-assembler-times or[ql] 1
FAIL: gcc.target/i386/stack-check-19.c scan-assembler-times (?:je|jne) 3
FAIL: gcc.target/i386/stack-check-19.c scan-assembler-times or[ql] 2
FAIL: gcc.target/i386/sw-1.c scan-rtl-dump pro_and_epilogue "Performing shrink-wrapping"
FAIL: gcc.target/i386/stackalign/pr88483-1.c -mno-stackrealign  scan-assembler-not (sub|add)(l|q)[\\\\t ]*\\\\\$[0-9]*,[\\\\t ]*%[re]?sp
FAIL: gcc.target/i386/stackalign/pr88483-1.c -mno-stackrealign  scan-assembler-not and[lq]?[^\\\\n]*-[0-9]+,[^\\\\n]*sp
FAIL: gcc.target/i386/stackalign/pr88483-1.c -mstackrealign  scan-assembler-not (sub|add)(l|q)[\\\\t ]*\\\\\$[0-9]*,[\\\\t ]*%[re]?sp
FAIL: gcc.target/i386/stackalign/pr88483-1.c -mstackrealign  scan-assembler-not and[lq]?[^\\\\n]*-[0-9]+,[^\\\\n]*sp
FAIL: gcc.target/i386/stackalign/pr88483-2.c -mno-stackrealign  scan-assembler-not and[lq]?[^\\\\n]*-[0-9]+,[^\\\\n]*sp
FAIL: gcc.target/i386/stackalign/pr88483-2.c -mstackrealign  scan-assembler-not and[lq]?[^\\\\n]*-[0-9]+,[^\\\\n]*sp
```

## Failures due to default PIE

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
