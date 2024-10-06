---
abbrlink: ''
categories: []
copyright_author: Tony
copyright_author_href: https://blog.iamsjy.com/
copyright_info: 此文章版权归Tony所有，如有转载，请注明来自原作者
copyright_url: https://blog.iamsjy.com/2022/10/04/deploy-umami-analytics-on-vercel/
index_img: https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/blog-image/umami-vercel.webp
date: '2023-08-22T17:06:04.088431+08:00'
tags: []
title: 【转载】在 Vercel 部署 umami 网站统计及报错解决
updated: '2024-08-18T23:04:06.114+08:00'
---
# 转载

**本文转载于 [在 Vercel 部署 umami 网站统计及报错解决 | Tony's Blog (iamsjy.com)](https://blog.iamsjy.com/2022/10/04/deploy-umami-analytics-on-vercel/)，遵循 [CC BY 4.0 协议](https://creativecommons.org/licenses/by/4.0/deed.zh).**

**原文作者：Tony**

**原文链接：** https://blog.iamsjy.com/2022/10/04/deploy-umami-analytics-on-vercel/

## 导入

Umami 是一种简单、快速的网站分析替代品，可替代 Google Analytics。

注：本文前两部分转载于 Lemonawa’s Blog，遵循 CC BY 4.0 协议，报错解决部分为原创。

## 准备

一个GitHub账号

一个Vercel账号（可直接由GitHub登录）

一个supabase账号（可直接由GitHub登录）

## 部署

访问umami的代码仓库，将其Fork至自己的账户中。

登录supabase，单击New Project来新建一个数据库，根据提示设置数据库名称和密码。

![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/8/image_f75e98c762deb9acd3f82a8775488231.png](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/8/image_f75e98c762deb9acd3f82a8775488231.png)

进入刚刚新建的Project，点击左边的SQL Editor（命令图标）- New query来新建查询，并将此处的命令全部复制到框中，随后点击RUN，看见Success即可。

![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/8/image_1b20be42f32e15cbb185f7a205a8a76a.png](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/8/image_1b20be42f32e15cbb185f7a205a8a76a.png)

然后打开Vercel，登录，点击New Project，在左侧选中Fork的项目，点击Environment Variables来设置环境变量：

 ![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/8/image_0818371b6ab29d2d828b547b89d13ac7.png](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/8/image_0818371b6ab29d2d828b547b89d13ac7.png)

DATABASE_URL: postgresql://postgres:[YOUR-PASSWORD]@[Your-URI]:5432/postgres（在supabase project-左侧设置-Database-Connection string-URI获得）

HASH_SALT: 随机英文字符串（滚键盘）

然后点击部署，部署完成后会给一个域名，点击即可进入

用户名：admin

默认密码：umami

## 报错解决

你需要准备一台 Linux x86 VPS（不能是 arm64）。如果没有，建议使用 GitHub Codespaces 来操作。

以下是详细步骤：

数据库连接失败（Unable to connect to the database）

请检查 Vercel 环境变量中 DATABASE_URL 的值是否填写正确，有没有多加 DATABASE_URL。修改后重新部署即可。

数据库连接失败（A migration failed to apply.）

将你 fork 的 umami 仓库 clone 到本地，并进入仓库目录。

git clone https://github.com/[你的 GitHub 用户名]/umami && cd umami

在本地 umami 目录中创建一个 .env 文件，填入 DATABASE_URL= ，后面粘贴数据库连接地址（与 Vercel 环境变量中 DATABASE_URL 的值相同，可以直接复制过来）。

在本地 umami 目录中执行以下命令：

yarn install

yarn build

检查详细d报错信息，并根据不同的报错执行不同的修复命令

如果是 02_add_event_data 错误则执行以下命令

yarn prisma migrate resolve --applied "02_add_event_data"

如果是 03_remove_casade_delete 错误则执行以下命令

yarn prisma migrate resolve --applied "03_remove_casade_delete"

等待命令执行完成，提示 Success! 则表示成功。
