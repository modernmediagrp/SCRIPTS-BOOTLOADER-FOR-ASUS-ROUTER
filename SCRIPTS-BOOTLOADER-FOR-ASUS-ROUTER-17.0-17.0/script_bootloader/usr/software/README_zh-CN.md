# Readme for software

## 前言

1. 本插件是开发插件所需的代码参考实例，并无实际功能
2. 本文档是开发插件所需的文档参考实例，除本节（即**前言**）外，其它均为参考实例。换言之，在真实的插件文档中，不应包含**前言**段

## 概述

1. *本插件功能1*
2. *本插件功能2*

## 安装前提

1. *前提1*
2. *前提2*

## 文件结构

`ASUS_ROUTER/script_bootloader/usr/自定义程序名（本例中为software）/`（自定义程序，即插件的全部文件）

| 权限      | 名称            | 属性     | 说明                         |
| --------- | --------------- | -------- | ---------------------------- |
| rwxrwxrwx | README_zh-CN.md | 普通文件 | （**必选**）说明文件         |
| rwxrwxrwx | bin             | 目录     | （**必选**）可执行文件目录   |
| rwxrwxrwx | etc             | 目录     | （**可选**）配置文件目录     |
| rwxrwxrwx | tmp             | 目录     | （**可选**）临时文件目录     |
| rwxrwxrwx | usr             | 目录     | （**可选**）外部软件资源目录 |
| rwxrwxrwx | var             | 目录     | （**可选**）可变文件目录     |

`ASUS_ROUTER/script_bootloader/usr/自定义程序名（本例中为software）/bin/`（此程序可执行文件目录）

| 权限      | 名称                     | 属性     | 说明                                       |
| --------- | ------------------------ | -------- | ------------------------------------------ |
| rwxrwxrwx | software_install         | 普通文件 | （**可选**）安装文件                       |
| rwxrwxrwx | software_enable.service  | 普通文件 | （**必选**）插件的可执行程序，用于启动程序 |
| rwxrwxrwx | software_disable.service | 普通文件 | （**必选**）插件的可执行程序，用于结束程序 |

`ASUS_ROUTER/script_bootloader/usr/自定义程序名（本例中为software）/etc/`（此程序配置文件目录）

| 权限      | 名称          | 属性     | 说明                 |
| --------- | ------------- | -------- | -------------------- |
| rwxrwxrwx | software.conf | 普通文件 | （**可选**）配置文件 |

`ASUS_ROUTER/script_bootloader/usr/自定义程序名（本例中为software）/tmp/`（此程序临时文件目录）

| 权限      | 名称         | 属性     | 说明                 |
| --------- | ------------ | -------- | -------------------- |
| rwxrwxrwx | software.tmp | 普通文件 | （**可选**）临时文件 |

`ASUS_ROUTER/script_bootloader/usr/自定义程序名（本例中为software）/usr/`（此程序外部软件资源目录）

| 权限      | 名称     | 属性     | 说明                                             |
| --------- | -------- | -------- | ------------------------------------------------ |
| rwxrwxrwx | software | 普通文件 | （**可选**）外部软件资源：含二进制文件、库文件等 |

`ASUS_ROUTER/script_bootloader/usr/自定义程序名（本例中为software）/var/`（此程序可变文件目录）

| 权限      | 名称         | 属性     | 说明                 |
| --------- | ------------ | -------- | -------------------- |
| rwxrwxrwx | software.var | 普通文件 | （**可选**）可变文件 |


## 安装方法

执行`/tmp/mnt/ASUS_ROUTER/script_bootloader/usr/software/bin/software_install`。程序会根据路由器架构，自动安装适当版本的software

   > [受支持的路由器型号](https://github.com/Entware/Entware/wiki/Install-on-Asus-stock-firmware)：
   >
   > | 架构        | 路由器型号                                                                                                                                                        |
   > | ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
   > | **aarch64** | GT-AC2900, GT-AC5300, GT-AX11000, RT-AC86U, RT-AX88U, RT-AX92U                                                                                                    |
   > | **armv7**   | Lyra Voice, RT-AC56U, RT-AC66U B1, RT-AC68P, RT-AC68U, RT-AC87U, RT-AC88U, RT-AC1200G, RT-AC1900P, RT-AC3100, RT-AC3200, RT-AC5300, RT-ACRH13, RT-AX56U, RT-AX58U |
   > | **mipsel**  | RT-N16, RT-N56U, RT-N66R, RT-N600, RT-AC51U, RT-AC66U, RT-AC66R, RT-AC1200, RT-AC1750, RT-AC1750 B1                                                               |

## 调用方法

| 插件文件                 | 插件调用者                   | 调用位置                                                                 |
| ------------------------ | ---------------------------- | ------------------------------------------------------------------------ |
| software_enable.service  | list_of_user_custom_scripts  | 第46行（安装后需手动配置开机加载。启用：删除行首`#`；禁用：恢复行首`#`） |
| software_disable.service | script_bootloader_usb_umount | 自动调用                                                                 |