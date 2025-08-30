---
layout: post
title:  "SIMD in ARM"
date:   2019-06-08 12:32:45 +0100
categories: [dav1d]
---

So now let's talk about the project I am working on but before further proceedings let me remind about the tutorial to [refer](https://thinkingeek.com/arm-assembler-raspberry-pi/) to, if you have understood those or already know about ARM assembly then we are on the same page.

My project is "dav1d ARM NEON optimization" and, I have applied under GSoC'19 program and the project is initiated and maintained by VideoLAN and FFmpeg. So dav1d is an av1 decoder which like any other decoder aspires to be fast and efficient. It is available for x86, x64, ARMv7, ARMv8 architectures, my project deals with ARM arch specifically ARMv7-a. So to make code exec efficient and fast we need to cut-off in between generalised high-level language compiler and directly talk with assembly lang to the processor(communication with a native language on a country land will always be a fine interpretation to that of foriegn language). It makes code development bit tough but trust me when you see the difference, it's all worth the patience, time and effort.

Now, we are not just writing assembly code for the different filters and functions of decoder but as humans, we never settle for less, so we exploit some extra functionalities.

There are a total of 16  registers, we denote it with R and a CPSR in the processor. We also got a co-processor, we use SIMD instruction with following floating point registers sets and execute single instruction on multiple data(SIMD).

![](http://infocenter.arm.com/help/topic/com.arm.doc.dht0002a/graphics/advanced_simd_and_vfp_register_set.svg)

So now I am gonna demonstrate an example to get clear about how things really work.

C Code
```c
for(int i=0;i<4;i++)
    c[i]=a[i]+b[i];
```
Corresponding assembly code with general purpose registers

```
.data
a:
    .int 4, 4, 4, 4
b:
    .int 8, 8, 8, 8
c:
    .int 0, 0, 0, 0

.text
.global main
main:
    ldr r0,addr_a
    ldr r1,addr_b
    ldr r2,addr_c
    mov r4,#3
loop:
    cmp r4,#0
    beq end
    ldr r5,[r0]
    ldr r6,[r1]
    ldr r7,[r2]
    add r7,r5,r6
    str r7,[r2]
    add r0,r0,#4
    add r1,r1,#4
    add r2,r2,#4
    sub r4,#1
    b loop
end:
    bx lr

addr_a: .word a
addr_b: .word b
addr_c: .word c
```
Assembly code with SIMD
```

.data
a:
    .int 4, 4, 8, 8
b:
    .int 8, 8, 8, 8
c:
    .int 0, 0, 0, 0

.text
.global main
main:
    ldr r0,addr_a
    ldr r1,addr_b
    ldr r2,addr_c
    vld1.8 {q0},[r0]!
    vld1.8 {q1},[r1]!
    vadd.I8 q2,q0,q1 // operated on multiple data at once
    vst1.8 {q2},[r2]!// hence loop not required to iterate
    bx lr            // through each element

addr_a: .word a
addr_b: .word b
addr_c: .word c
```
So in regards with assembly with SIMD, we need not loop at all, we are executing the instruction on 4 int type data at once. Hence if need to loop 16 times in C code, we need to only go for 4 with SIMD implementation. We also do some reordering with instructions and loop unrolling to even more optimize the code. I will share tricks and tips in the upcoming blog posts.

In the next blog post, I would start sharing my weekly progress and we will have an insight into the dav1d functions and implementations
