---
layout: post
title:  "Building Haiku and emulating with Qemu for Linux Distros"
description:
date:   2018-03-24 10:51:47 +0530
tag:
- Kernel
- OS
- Haiku
- Qemu
categories: [haiku]
---

## Building Haiku from source code

The following instructions are specifically to building haiku for x86_64 but you can always try building for other architectures too.

### Clonning the source code

The official repository seems broken anyway didn't work out for me so I clonned from github repo
```
git clone https://github.com/haiku/haiku.git
```
Haiku uses some external tools to build from the source code

```
git clone https://github.com/haiku/buildtools.git
```
make sure that both the clonned repositories are in the same directories

### Compiling buildtools

Create a directory where you are going to save the build image and related files

```
mkdir generated.x86_64; cd generated.x86_64
```
For compiling
```
../configure --build-cross-tools x86_64 ../../buildtools
```
### Building the image

Before building the image you need to install some dependencies

```
sudo apt-get install git nasm autoconf automake texinfo flex bison gawk build-essential unzip wget zip less zlib1g-dev libcurl4-openssl-dev genisoimage libtool
```
Aditional requirements for ARM

```
sudo apt-get install u-boot-tools util-linux mtools device-tree-compiler bc
```
For creating nightly anyboot Haiku iso image

```
jam -q -j2 @nightly-anyboot
```
For creating nightly raw disk images
```
jam -q -j2 @nightly-raw
```
### Error

Now if you getting an error while building, specifically about haiku revision.
Then,
```
cd $home/haiku/build/jam
```
```
cat UserBuildConfig
```
Now copy hrexxxxx, and go to haiku/generated.x86_64/build
```
cd $home/haiku/generated.x86_64/build
```
Then created and write into the file
```
echo -n "hrevxxxxx" > haiku-revision
```
Your error will be fixed
## Emulation with Qemu

### Installing Qemu

Qemu is a software in which you can emulate various hardware and on top of that you can run OS in vitual enviornment

```
sudo apt-get install qemu
```
### Booting OS in virtual drive

Now create an virtual harddrive in which you are going to boot the OS
```
qemu-img create haiku-vm.img 10G
```
Now boot the OS in the virtual drive
```
sudo qemu-system-x86_64 -boot d -cdrom haiku/generated.x86_64/haiku-nightly-anyboot.iso -m 512 -hda haiku-vm.img
```
Now you can simply run the virtual drive
```
sudo qemu-system-x86_64 haiku-vm.img
```

If you have any issues with building and emulation, feel free to comment :)

Hope this helps!
