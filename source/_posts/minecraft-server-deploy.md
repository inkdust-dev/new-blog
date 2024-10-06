---
abbrlink: ''
categories:
- - 技术教程
index_img: https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/blog-image/minecraft-server-deploy.png
date: '2024-04-05T18:18:15.056891+08:00'
tags:
- Minecarft
- 游戏
- 私有化
title: 基于Win Server部署Minecraft服务器
updated: '2024-08-07T22:32:44.925+08:00'
---
## 介绍

**《我的世界》**（Minecraft）是一款沙盒类电子游戏，由马库斯·阿列克谢·泊松（Notch）创作。游戏由Mojang Studios维护，现属微软Xbox游戏工作室。最初于2009年5月17日发布Classic版本，2011年11月18日推出Java正式版。游戏可在桌面设备、移动设备和游戏主机上运行。中国版目前由网易游戏代理，自2016年5月20日起在中国大陆运营。

在延斯·伯根斯坦（Jeb）加入并负责开发之前，Notch几乎独自完成了《我的世界》的开发工作。游戏音乐由丹尼尔·罗森菲尔德（C418）和莉娜·雷恩（Lena Raine）创作；克里斯托弗·泽特斯特兰绘制了游戏中的画。

游戏的核心玩法是让玩家在充满方块的三维空间中自由创造和破坏各种方块。玩家可以在单人或多人模式下摧毁或建造复杂的建筑和艺术品，或者收集物品探索地图以完成游戏的成就。此外，在创造模式下，玩家还可以尝试使用红石电路和指令等功能。

——摘自百度百科

{% note danger %}

该教程仅适用于Java版本的Minecraft游戏，不适用于网易版《我的世界》、基岩版Minecraft。

{% endnote %}

## 测试环境

处理器	Intel(R) Xeon(R) CPU E5-2696 v4 @ 2.20GHz   2.20 GHz  (4 个处理器)
机带 RAM	8.00 GB
设备 ID	F6EB2C89-0238-491C-BA33-7922E889987D
产品 ID	00455-10000-00000-AAOEM
系统类型	64 位操作系统, 基于 x64 的处理器
笔和触控	没有可用于此显示器的笔或触控输入

版本	Windows Server 2022 Datacenter
版本号	21H2
安装日期	‎2024/‎3/‎26
操作系统内部版本	20348.2340

## Java环境安装

来到Oracle官网安装Java环境。[Java Downloads | Oracle 中国](https://www.oracle.com/cn/java/technologies/downloads/)

本教程使用JDK22作为演示环境。下载地址：

| Product/file description | File size | Download                                                                                                                                                                                                                            |
| ------------------------ | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| x64 Compressed Archive   | 185.52 MB | [https://download.oracle.com/java/22/latest/jdk-22\_windows-x64\_bin.zip](https://download.oracle.com/java/22/latest/jdk-22_windows-x64_bin.zip) ([sha256](https://download.oracle.com/java/22/latest/jdk-22_windows-x64_bin.zip.sha256)) |
| x64 Installer            | 163.91 MB | [https://download.oracle.com/java/22/latest/jdk-22\_windows-x64\_bin.exe](https://download.oracle.com/java/22/latest/jdk-22_windows-x64_bin.exe) ([sha256](https://download.oracle.com/java/22/latest/jdk-22_windows-x64_bin.exe.sha256)) |
| x64 MSI Installer        | 162.07MB  | [https://download.oracle.com/java/22/latest/jdk-22\_windows-x64\_bin.msi](https://download.oracle.com/java/22/latest/jdk-22_windows-x64_bin.msi) ([sha256](https://download.oracle.com/java/22/latest/jdk-22_windows-x64_bin.msi.sha256)) |

如果你的服务器出于中国境内，或在此页面下载缓慢，可以尝试使用Injdk下载。

Injdk地址：[OracleJDK](https://injdk.cn/#oracle-jdk)

JDK22下载地址：

| Product/file description | File size | Download                                                                                                                                                                                                                                                                     |
| ------------------------ | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| x64 Compressed Archive   | 185.52 MB | [https://d6.injdk.cn/oraclejdk/22/jdk-22_windows-x64_bin.zip]([https://d6.injdk.cn/oraclejdk/22/jdk-22_windows-x64_bin.zip](https://d6.injdk.cn/oraclejdk/22/jdk-22_windows-x64_bin.zip)) ([sha256](https://download.oracle.com/java/22/latest/jdk-22_windows-x64_bin.zip.sha256)) |
| x64 Installer            | 163.91 MB | [https://d6.injdk.cn/oraclejdk/22/jdk-22_windows-x64_bin.exe](https://d6.injdk.cn/oraclejdk/22/jdk-22_windows-x64_bin.exe) ([sha256](https://download.oracle.com/java/22/latest/jdk-22_windows-x64_bin.exe.sha256))                                                               |
| x64 MSI Installer        | 162.07MB  | [https://d6.injdk.cn/oraclejdk/22/jdk-22_windows-x64_bin.msi](https://d6.injdk.cn/oraclejdk/22/jdk-22_windows-x64_bin.msi) ([sha256](https://download.oracle.com/java/22/latest/jdk-22_windows-x64_bin.exe.sha256))                                                               |

![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_fe44aa71038b03b1a92843ff66b698ed.png](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_fe44aa71038b03b1a92843ff66b698ed.png)

一直下一步即可。

安装完成后关闭弹窗即可。

在搜索框搜索“查看高级系统设置”，在其他版本的Windows上可能是“高级系统设置”，请注意识别

![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_1709db623d6aa13a1ccf097e0e58ce7f.png](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_1709db623d6aa13a1ccf097e0e58ce7f.png)

打开后选择环境变量，新建一个用户变量。

变量名为 `JAVA_HOME`

变量值为你的Java安装路径，如果你安装时未选择安装路径，请填写 `C:\Program Files\Java\jdk-22`

如果你安装时已选择安装路径，请填写为你安装选择的路径

![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_88cab5786fba2733702e956581bd449f.png](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_88cab5786fba2733702e956581bd449f.png)

双击系统变量中的Path变量（如未找到请向下滑动），新建一个环境变量：`%JAVA_HOME%\bin`

![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_08bed54b5c5c36d2ff211f0e99d5c3ae.png](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_08bed54b5c5c36d2ff211f0e99d5c3ae.png)

添加好变量后，按Win + R输入 `cmd`打开命令提示符。输入 `java -version`，出现版本号即代表环境配置完成。

![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_f3a40b8ab04323e7836190df9fdb88ce.png](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_f3a40b8ab04323e7836190df9fdb88ce.png)

## Minecraft Server端安装

通过Minecraft官网下载Java版本Server端。

[Download server for Minecraft | Minecraft](https://www.minecraft.net/zh-hans/download/server)

如果你打不开Minecraft官网，可点击[minecraft_server.1.20.4.jar](https://piston-data.mojang.com/v1/objects/8dd1a28015f51b1803213892b50b7b4fc76e594d/server.jar)下载1.20.4版本的Server端。

![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_1135144edd37d1b56adec4b769f1ab88.png](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_1135144edd37d1b56adec4b769f1ab88.png)

下载后双击打开，并修改生成的eula文件中的“elua=false”为

```plaintext
elua=true
```

如果你没有正版账号，请修改“server.properties”文件中的online-mode为false。

![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_4e0af366d6a00236eb6ad5af38ba47a4.png](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_4e0af366d6a00236eb6ad5af38ba47a4.png)

然后点击地址栏，输入“cmd”打开命令提示符，输入：

```plaintext
java -jar server.jar --nogui
```

即可建立属于你自己的Minecraft服务器。地址即为：[ip]:25565

## 安装客户端

{% note danger %}

安装客户端不需要在服务器上安装，请在游玩的电脑上安装。

{% endnote %}

如果您已购买Minecraft服务器，您可以安装第三方客户端登陆。

如果你想不购买Minecraft即可游玩该游戏，您需要安装第三方客户端游玩。

以第三方启动器PCL2为例子：

### 下载PCL2

开发者创作不易，如有条件可发电支持。

[PCL 正式版下载丨龙腾猫跃丨爱发电](https://afdian.net/p/0164034c016c11ebafcb52540025c377)

最新正式版永久下载地址

**下载地址** 1：[https://ltcat.lanzoum.com/b0aj6gsid](https://ltcat.lanzoum.com/b0aj6gsid)（提取码：pcl2）

**下载地址** 2：[https://pan.baidu.com/s/1f7ipEIkZeMNmGSs\_fu2YoA?pwd=pcl2](https://pan.baidu.com/s/1f7ipEIkZeMNmGSs_fu2YoA?pwd=pcl2)（提取码：pcl2）

下载后双击“Plain Craft Launcher 2.exe”即可。可在PCL2中安装MC、Mod、Fabric、Forge、Optifine等等。

![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_204337b6bfac7022855d583fbcdbdc8c.png](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_204337b6bfac7022855d583fbcdbdc8c.png)

如果在过程中出现安装MC出现问题，请参考下方内容进行解决。

### MC下载问题

由于受到 MCBBS 关站影响，由 MCBBS 提供服务的 MCBBS 国内源也已关闭。MCBBS 源是国内最大的 Minecraft 镜像下载源，所以PCL2启动器因此受影响，您可以更新PCL2版本来解决该问题。

如无法获取版本列表。

您可在PCL 2中的设置——个性化——下载——版本列表中选择尽量使用官方源。

![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_86c5ea6aa39d597248b6f40fa7e9b97c.png](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/4/image_86c5ea6aa39d597248b6f40fa7e9b97c.png)
