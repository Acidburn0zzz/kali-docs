---
title: NanoPi NEO Plus2
description:
icon:
type: post
weight:
author: ["steev",]
build-script: https://gitlab.com/kalilinux/build-scripts/kali-arm/-/blob/master/nanopineoplus2.sh
build-script: https://gitlab.com/kalilinux/build-scripts/kali-arm/-/blob/master/nanopineoplus2-minimal.sh
headless: kali-desktop-xfce
metapackage: kali-linux-default
status: pre-generated
cpu:
gpu:
ram:
ethernet:
wifi:
bluetooth:
usb3:
usb2:
storage:
---

The [NanoPi NEO Plus2](http://nanopi.io/nanopi-neo-plus2.html) has an Allwinner H5, Quad Core Cortex™-A53 (ARMv8 64-bit) processor with Triple Core Mali-450 MP4 GPU and 1GB DDR3 RAM. The NanoPi NEO Plus2 has an 8GB eMMC, which is too small for a default Kali installation, so we run from an external microSD card.

By default, the Kali Linux NanoPi NEO Plus2 image contains the [**kali-linux-default** metapackage](https://tools.kali.org/kali-metapackages) similar to most other platforms. If you wish to install extra tools please refer to our [metapackages page](/docs/general-use/metapackages/).

## Kali on NanoPi NEO Plus2 microSD card - User Instructions

If you're unfamiliar with the details of [downloading and validating a Kali Linux image](/docs/introduction/download-official-kali-linux-images/), or for [using that image to create a bootable device](/docs/usb/live-usb-install-with-windows/), it's strongly recommended that you refer to the more detailed procedures described in the specific articles on those subjects.

To install a pre-built image of the standard build of Kali Linux on your NanoPi NEO Plus2, follow these instructions:

1. Get a fast microSD card with at least 16GB capacity. Class 10 cards are highly recommended.
2. Download _and validate_ the `Kali NanoPi NEO Plus2` image from the [downloads](https://www.offensive-security.com/kali-linux-arm-images/) area. The process for validating an image is described in more detail on [Downloading Kali Linux](/docs/introduction/download-official-kali-linux-images/).
3. Use the **[dd](https://packages.debian.org/testing/dd)** utility to image this file to your microSD card (same process as [making a Kali USB](/docs/usb/live-usb-install-with-windows/).

In our example, we assume the storage device is located at `/dev/sdb`. Do _not_ simply copy these value, **change this to the correct drive path**.

{{% notice info %}}
This process will wipe out your microSD card. If you choose the wrong storage device, you may wipe out your computers hard disk.
{{% /notice %}}

```console
$ xzcat kali-linux-$version-nanopineoplus2.img.xz | sudo dd of=/dev/sdb bs=4M status=progress
```

This process can take a while, depending on your PC, your microSD card's speed, and the size of the Kali Linux image.

Once the _dd_ operation is complete, boot up the NanoPi NEO Plus2 with the microSD card plugged in.

You should be able to [log in to Kali](/docs/introduction/default-credentials/).

## Kali on the NanoPi NEO Plus2 - Tips

The NanoPi NEO Plus2 will attempt to boot from the microSD card first if one is plugged in.

The wireless chipset is an Ampak AP6210, which is a rebranded Cypress (formerly Broadcom) Wireless card, so enterprising users may be able to get [nexmon](https://github.com/seemoo-lab/nexmon) working, if the work was put in.

If you want to change boot arguments/the kernel command line, you will need to edit the `/boot/boot.cmd` file, and then run `mkimage -C none -A arm -T script -d /boot/boot.cmd /boot/boot.scr`.

## Kali on NanoPi NEO Plus2 - Image Customization

If you want to customize the Kali NanoPi NEO Plus2 image, including changes to the [packages](/docs/general-use/metapackages/) being installed, changing the [desktop environment](/docs/general-use/switching-desktop-environments/), increasing or decreasing the image file size or generally being adventurous, check out the [Kali-ARM Build-Scripts](https://gitlab.com/kalilinux/build-scripts/kali-arm) repository on GitLab, and follow the _README.md_ file's instructions. The script to use is `nanopineoplus2.sh`.