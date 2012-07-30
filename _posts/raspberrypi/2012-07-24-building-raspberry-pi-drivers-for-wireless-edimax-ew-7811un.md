---
layout: post
title: "Building Raspberry Pi drivers for Wireless Edimax EW 7811UN"
description: ""
category: Raspberry Pi
tags: [arch, linux, raspberrypi, wireless, edimax]
---
{% include JB/setup %}

At some point I decided that it would be excellent if my Raspberry Pi was not
bound by the shackles of ethernet cabling, and therefore after much
deliberation I purchased the Edimax EW7811un. 

This looked like an ideal piece of kit, and I knew from experience that Edimax
devices were usually quite compatible with Linux, and for < £5 where could I go
wrong? 

Unfortunately it has taken me several attempts to install the modules for the
wireless device. Although several solutions have been created for easy
installation on other Raspberry Pi operating systems (all withint Googlable
distance), no solution immediately presents itself for Arch.

After various levels of trial and error, I discovered that the following steps
must be taken to build the drivers for Arch. I hope this information is able to
help others with the same issue.

## Prerequisites

- Download the driver sources from the [Edimax website][1]. These allow the
  driver to be built from source.

- Install the Raspberry Pi kernel headers. For some reason the driver looks for
  the headers at a symlink that points to an incorrect location. So we must
  also recreate that link. Replace the kernel versions with the installed ones.

    sudo pacman -S raspberrypi-kernel-headers
    sudo ln -s /lib/modules/3.1.9-30-ARCH+/build /usr/src/linux-3.1.9-30-ARCH+

## Patching

The driver sources are based on an older kernel version, so we need to do some
patching.

Unzip and untar the driver sources

    unzip rtl8192CU_8188CU_linux_v2.0.939.20100726.zip
    cd rtl8192CU_8188CU_linux_v2.0.939.20100726/driver
    tar xzf rtl8192CU_linux_v2.0.939.20100726.tar.gz

Edit `include/rtw_xmit.h` and add the following include:

    #include <linux/interrupt.h>

Edit `os_dep/osdep_service.c` and add:

    #include <linux/semaphore.h>
    #define init_MUTEX(sem) sema_init(sem, 1)

Add a new platform to the `MakeFile`
    
    ifeq ($(CONFIG_PLATFORM_PI), y)
    EXTRA_CFLAGS += -DCONFIG_LITTLE_ENDIAN
    ARCH := arm
    CROSS_COMPILE := arm-bcm2708-linux-gnueabi-
    KVER := 3.1.9-30-ARCH+
    KSRC := ~/pi-sources
    MODDESTDIR :=
    ~/pi-sources/lib/modules/3.1.9-30-ARCH+/kernel/drivers/net/wireless/
    endif

## Building

To build the module run:

    make CONFIG_PLATFORM_PI=y modules.


  [1]: http://www.edimax.co.uk/en/support_detail.php?pd_id=328&pl1_id=1&pl2_id=44#01
