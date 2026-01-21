---
title: 编译内核
date: 2023-02-09 14:35:28
tags: ['Linux', 'Kernel']
categories: Linux
toc: true
excerpt: 编译内核
---
# 编译内核：
1. 安装相关依赖：`sudo apt-get install libncurses5-dev libncursesw5-dev libssl-dev bison flex`等。
2. 配置
```bash
cd /usr/src/linux-5.15.81
sudo make menuconfig
sudo vim .config
```
搜索`"debian/canonical-certs.pem"`和`"debian/canonical-revoked-certs.pem"`，并都改成`""`。

3. 编译
```bash
sudo make -j6
sudo make modules_install
sudo make install
sudo update-grub
reboot
```
