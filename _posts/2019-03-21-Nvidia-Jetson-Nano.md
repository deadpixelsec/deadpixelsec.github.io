---
layout: post
title: NVIDIA Jetson Nano
---
[@b34rd_tek](https://twitter.com/b34rd_tek)

The new single board computer (sbc) from Nvidia looks to be a promising new addition to hobbyists, hackers, and IoT developers alike! The specifications for the device were initially a bit of a mixed bag as the announcement said one thing, the website said another, and the engineers on developer forums had a different list. 

Here's the fully up-to-date details:

[NVIDIA Jetson Details](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-nano/)

### [](#header-3)Technical Specifications

|  Component   | Details
|:-------------|:------------------|
| GPU           | NVIDIA Maxwell™ architecture with 128 NVIDIA CUDA® cores |
| CPU           | Quad-core ARM® Cortex®-A57 MPCore processor              |
| Memory        | 4 GB 64-bit LPDDR4                                       |
| Storage       | 16 GB eMMC 5.1 Flash                                     |
| Video Encode  | 4K @ 30 (H.264/H.265)                                    |
| Video Decode  | 4K @ 60 (H.264/H.265)                                    |
| Camera        | 12 lanes (3x4 or 4x2) MIPI CSI-2 DPHY 1.1 (1.5 Gbps)     |
| Connectivity  | Gigabit Ethernet                                         |
| Display       | HDMI 2.0 or DP1.2  eDP 1.4  DSI (1 x2) 2 simultaneous    |
| UPHY          | 1 x1/2/4 PCIE, 1x USB 3.0, 3x USB 2.0                    |
| I/O           | 1x SDIO / 2x SPI / 6x I2C / 2x I2S / GPIOs               |
| Size          | 69.6 mm x 45 mm                                          |
| Mechanical    | 260-pin edge connector                                   |

### [](#header-3)Performance Benchmarks

NVIDIA shared some performance numbers as well. We should obviously take these with a grain of salt since these have not been validated in any way.

![alt text](https://devblogs.nvidia.com/wp-content/uploads/2019/03/imageLikeEmbed.png "Performance Graph")

### [](#header-3)Overall Thoughts

I know this information is short and doesn't really tell us much. For $99 this is an SBC that is priced between the Raspberry Pi and the Latte Panda with performance in line with pricing. I look at this personally as a Raspberry Pi with a better GPU that can be used for all sorts of extra tasks. It's advertised to be an AI device for embedded designers and researchers. I would love to see an OpenCL ICD. With that this device can be used to drop in a location, or even carry in a backpack while visiting a site and we can set it up to grab wifi handshakes and use cuda acceleration with pyrit to crack WPA2. We could also potentially cluster the devices together and use them as a lower power hashcat/machine learning setup, still in a backpack. There is a lot of potential here. Hopefully it delivers.

