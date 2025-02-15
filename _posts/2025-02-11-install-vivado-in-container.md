---
title: 'How to install Vivado in Docker container'
date: 2025-02-15
permalink: /posts/2025/02/install-vivado-in-container/
tags:
  - Docker
  - Vivado
---

This is a blog about how to install the newest `Vivado 2024.1` in Docker container.

# preparation

First, you should install [`Docker`](https://docs.docker.com/engine/install/ubuntu/) and [`Vivado` install package](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vivado-design-tools.html).

Notice that the `Vivado 2024.1` and the `Edition Update 1` will utilize about 140 GB disk storage. And after they are tared, they will utilize about 150 GB. So you had better prepare a disk with greater than 512 GB.

# Installation

Assume your packages path on your host machine is `/host/path/vivado-install/` and you mount them to container path `/xilinx/package`

For simplicity, here I first tar the Vivado package and directly mount the tared Vivado package.

```bash
cd /host/path/vivado-install/

tar xzf FPGAs_AdaptiveSoCs_Unified_2024.1_0522_2023.tar.gz 

tar xzf Vivado_Vitis_Update_2024.1.1_0614_1525.tar.gz
```

## run container

```bash
docker run -it --name vivado-install -v /host/path/vivado-install/:/xilinx/package ubuntu:22.04 bash
```

## install dependencies

Here you create a new folder, and install all the dependencies packages.

```bash
mkdir /xilinx/data && \
apt-get update -y && \
apt-get install -y  libxext-dev \
                locales     \
                libxrender-dev \
                libxtst-dev \
                libtinfo-dev \
                libncursesw5-dev \
                libncurses5-dev   \
                wget            \
                git             \
                vim             \
                openssh-client  \
                curl            \
                build-essential && \
wget http://archive.ubuntu.com/ubuntu/pool/universe/n/ncurses/libtinfo5_6.4-2_amd64.deb && \
dpkg -i libtinfo5_6.4-2_amd64.deb && \
locale-gen "en_US.UTF-8" && \
update-locale LANG=en_US.UTF-8 && \
cd /xilinx/package
```

## install Vivado

Generate the `install_config.txt`

```bash
cd /xilinx/package/FPGAs_AdaptiveSoCs_Unified_2024.1_0522_2023/

./xsetup -b ConfigGen
```

Revise the `install_config.txt` based on your needs. Then run the install command.

```bash
./xsetup --agree XilinxEULA,3rdPartyEULA --batch Install --config ./install_config.txt
```

Also install the update package.

```bash
cd /xilinx/package/Vivado_Vitis_Update_2024.1.1_0614_1525

./xsetup --agree XilinxEULA,3rdPartyEULA --batch Install --config ./install_config.txt
```

## setup environment variables

```bash
echo 'export PATH=/tools/Xilinx/Vivado/2024.1/bin:$PATH' >> /root/.bashrc 

echo "source /tools/Xilinx/Vivado/2024.1/settings64.sh" >> /root/.bashrc
```

## verification

```bash
vivado -version

vivado -mode tcl
```

## build the container

```bash
docker ps

CONTAINER ID   IMAGE     COMMAND       CREATED        STATUS       PORTS     NAMES
4e5ced321e24   ubuntu    "/bin/bash"   16 hours ago   Up 4 hours             vivado-install
```

On your host machine, run :

```bash
docker commit vivado-install xilinx:latest
```

Check the image.

```bash
docker images
```
