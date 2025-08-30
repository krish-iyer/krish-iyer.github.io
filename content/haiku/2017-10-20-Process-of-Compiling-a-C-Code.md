---
layout: post
title:  "Process of Compiling a C-Code"
description:
date:   2017-10-20 10:51:47 +0530
tag:
- Compiler Processes
- C Programming
category: [randombin]
---
We program to give a certain set of instructions to the computer but it’s tough and time-consuming to learn machine code and give instructions. So we have developed a high-level language which is converted into a low-level language(machine code) through certain tools and each tool is specific to the hardware which is going to understand the instructions. The tool to convert C code into machine code is called as compilers. For general purpose and compiling codes for Linux we use gcc and for AVR microcontrollers we use avr–gcc and PIC-microcontrollers we have pic-gcc.

So when you write a programme these tools run some processes which to convert it into machine code. When we compile our code, the compiler takes ion the header file and checks if the code is syntactically right or wrong and then it is converted into a intermediate language which is equal to assembly code and then through an assembler, it is converted into the machine code or the executable .hex file.

The compiler has three parts:

Preprocessor: It adds header file contents in our code. It replaces text substitution labels and macros with their original values and it also removes comments and white spaces from the programme.

Parser: It creates tokens and makes sure that tokens are according to certain rules in C and it determines the actions must be taken by each expression and passes a list of instructions to the code generator.

Code Generator: It takes the list of instructions and translates into device specific assembly language instructions. This part of the compiler is different for every microcontroller.

Now the assembler converts the assembly code into machine code. After converting into the machine code the Linker talks with the hardware and knows that which part of the memory is allocated or free so that it can go back and replace variable and function names with the assigned memory.

It is always recommended to code in assembly though it is tough because the converted C code is not that optimised. For an example- you can write 30 lines of C programme which can require only 4 lines of assembly code. So to speak french is France rather than english but yeah english will work too.
