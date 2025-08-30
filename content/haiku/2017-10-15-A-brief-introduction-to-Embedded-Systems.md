---
layout: post
title:  "Introduction to Embedded Systems"
date:   2017-10-15 10:51:47 +0530
tag:
- Hardware
- Software
- Basics
category: [randombin] 
---
The first guess we make is of-course something small and which is a part of a big system. So I will try to convert all of your guesses to some fundamental knowledge so the next time you will more confident than just making a guess.

So yes, Embedded systems have software embedded inside the hardware. Hence it has two parts hardware and software. These systems are task specific and function & respond in real time. This hardware understands the language of 0 & 1 which we call as a low-level language, there are more of these like hexadecimal, octal number systems etc. These instructions in low-level languages are burned in the memory of the micro controllers or micro processors. Basically, micro controllers are made on based on two architecture, Harvard and Von Neumann. The basic difference in both the architecture is one of them( Von Neumann) got two sperate memories so that instructions and data, so they can be done simultaneously. The other one(Harvard) has only one memory so either it can give instruction or play with data at a time. So the hardware has millions of logic circuits and small switches which are actually flip-flops and are used make a register and it has a state(0 or 1) and some set of register will give you a series of 0 & 1 values which is a data or based on it state of registers current or data is been circulated and instructions.

So now our job is to burn this low-level language codes into the hardware but it’s hard to give instructions in low-level language so we have some set of tools(toolchain) which can convert high-level language(embedded C) into low-level, these tools actually are some compilers and assemblers. There are different compilers and assemblers for different hardware. You will write the code in embedded C and then you can convert this code to hex format using the tool chain and then by using a programmer you can burn the code in the hardware.

The micro controller is basically a micro processor with memory and we can’t add RAM, ROM, I/O ports etc externally. Now there are some sets or logics or programmes which are already written in the hardware they are called Static logics and there are logics which we can change in order to get the desired output and these are called new logics and these two logics are part of ASIP(Application-specific instruction set processor) and there’s also ASIC which has IC(integrated circuit). The embedded system is made of memory, ASIP&ASIC, processors core, Analog and Digital I/O. There are two processors in the system(Program flow control unit(CU) and Execution Unit(EU)). CU fetches the instructions from the memory and EU transfers the data and also do the data conversion it also contains ALU(Arithmetic Logical Unit).

Hope you guys got the over view about embedded systems. I will be updating more on different pages. Stay tuned 😉
