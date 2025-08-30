---
layout: post
title:  "Introduction to ARM Assembly and dav1d"
date:   2019-06-04 12:32:45 +0100
categories: [dav1d]
---

## General Assembly
The first thing to know about the assembly is, it's very much architecture dependant so for every different architecture there's a completely different story. Secondly, it's hard to get but that makes it more interesting. 

So before stepping into ARM assembly, I have written assembly programs and studied architecture in detail for mid-range micro-controllers. Also, I have done bit study for TMS320C6000 and TMS320F28027, they are like DSP processors so data lines and processor units are bit different there. 

## Why Assembly

Besides the fact that it makes you feel more closer to the hardware and you have more control over things like processor, co-processor, peripherals etc, it is also very efficient, so mostly you have seen assembly codes for small memory devices with comparatively low processing power. The best example would be [Kolibri OS](https://kolibrios.org/en/) which is forked from [Manuet OS](http://menuetos.net/) repo. 

It's ok if you explain French-speaking person in English but communicating in French would make things straight forward and wouldn't require much effort to understand on both the sides.

## How to get started with ARM Assembly

This [blog](https://thinkingeek.com/arm-assembler-raspberry-pi/) will get you to hang for a start, don't get afraid if you don't follow anything with first few blog posts, later it's all gonna make sense. Follow through the exercises and important part to focus would be Matrix Multiply and SIMD ones. Also, Roger will clear all your doubts, there might be some delay but it would be worth the patience.

Now arm assembly for ARMv7 and ARMv8 has some differences with the instruction, not to forget that they are 32bit and 64bit processor respectively, that might change the whole perspective of code implementation.

## dav1d NEON Optimization

[dav1d](https://code.videolan.org/videolan/dav1d) is an av1 decoder more about dav1d you can read from [j-b's blog](http://www.jbkempf.com/blog/post/2018/Introducing-dav1d). In order to achieve faster execution we need to optimize the code and also use some co-processor's capabilities to make it much more faster, so here comes NEON into play, it's built on co-processor 10 and 11(IIRC). So with this one, we get access to vector registers and we can execute single instruction on multiple data(SIMD).

I will share some of the benchmarks in upcoming blog posts which compares C implementation vs Assembly implementation.