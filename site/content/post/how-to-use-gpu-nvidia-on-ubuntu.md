---
title: How to use GPU Nvidia on Ubuntu
date: 2023-08-22T14:05:22.132Z
description: It's the drivers, and it's fast!
image: https://miro.medium.com/v2/resize:fit:3840/format:webp/1*MF7tYFn-m846_z-p3vBWxQ.png
---
## Installing CUDA Drivers on Ubuntu

#### Introduction to CUDA and its Applications

CUDA (Compute Unified Device Architecture) is a parallel computing platform and programming model developed by NVIDIA. It empowers developers to tap into the immense computational power of NVIDIA GPUs for accelerating a wide range of tasks. 

With CUDA, tasks that demand intensive parallel processing, such as deep learning, scientific simulations, and data analysis, can be performed dramatically faster. By leveraging the thousands of cores within a GPU, CUDA has revolutionized fields that require heavy computational lifting, making it a go-to solution for researchers, developers, and data scientists.

W﻿e're going to be following these steps:

1. E﻿nsure you have a Nvidia GPU available.
2. U﻿pdate your system
3. I﻿nstall latest nvidia drivers
4. D﻿isable default ubuntu drivers
5. I﻿nstall CUDA apps
6. V﻿erify installation

> V﻿ery easy way to keep up with new releases.

Follow these steps to install CUDA drivers on the latest Ubuntu:

1. **Check GPU Compatibility:**
   Ensure your GPU is compatible with the CUDA version you intend to install. Refer to NVIDIA's official documentation for compatibility details.

   Open up a terminal `Ctrl+Alt+T` and type

   ```shell
   lspci | grep -i nvidia
   ```

   T﻿he output should be shomething like this:

   ![nvidia checking](img/image_2023-08-22_164548862.png "Check if there is a Nvidia gpu in your system")

   I﻿f there is no output, then you don't have a Nvidia GPU. Sorry.

2. **Update System:**

   ```shell
   s﻿udo apt update
   s﻿udo apt upgrade -y
   ```

3. **Nvidia drivers:**
   I﻿nstructions from the official nvidia driver installation guide for ubuntu 22.xx found [here](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#ubuntu).

   ```shell
   sudo apt install linux-headers-$(uname -r)
   wget           https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.1-1_all.deb
   sudo dpkg -i cuda-keyring_1.1-1_all.deb
   sudo apt update
   sudo apt install cuda-drivers
   ```

4. **Disable default driver:**
   B﻿y disabling the default Nvidia driver from Canonical you will save a lot of trouble.

   ```shell
   echo -e "blacklist nouveau\noptions nouveau modeset=0" | sudo tee /etc/modprobe.d/blacklist-nouveau.conf
   sudo update-initramfs -u
   ```

5. **Reboot:**
   Reboot your system to apply the Nouveau driver changes.
6. **CUDA package installation:**
   W﻿ith all the steps above, you can safely copy&paste this code block.

   ```shell
   sudo apt install cuda
   ```

   ###### C﻿odeblock from deb&network installation on Ubuntu 22.04 from Nvidia [here](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_network).

7. **Reboot:**
   Reboot your system to get your CUDA up and running!

8. **Verifications:**
   T﻿he best way to check everything went well is to check **nvidia-smi**


   ```shell
   nvidia-smi
   ```

   T﻿he output should be like this, and with DRIVER VERSION and CUDA VERSION.

   ![nvidia-smi](img/image_2023-08-22_161926754.png "nvidia-smi")

> The package manager will automatically update everything. True Gold.

T﻿his is a wrap-up of the official Nvidia CUDA installation Guide for Linux, found [here](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)