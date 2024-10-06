---
abbrlink: ''
categories: []
index_img: https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/24/8/ltesencrypt-ssl_be3d1fad61002208589a66246d0a7e78.png
date: '2024-08-07T22:26:44.564178+08:00'
tags: []
title: SSL系列一之快速签发免费Let's Encrypt泛域名证书
updated: '2024-08-07T22:27:13.280+08:00'
---
## 引入

现如今，向像腾讯，阿里云等大厂的免费SSL证书，都由一年缩短为3个月。

[https://cloud.tencent.com/document/product/400/104538](https://cloud.tencent.com/document/product/400/104538)

在如今的形式下，签发免费的3个月的单域名证书显然不如直接签发Let's Encrypt、ZeroSSL等ACME提供的泛域名证书来的方便。

而acme.sh常用于Linux端上证书的自动化签发与续约，对于不使用服务器的人群，显然造成了许多麻烦，那么可以通过Web端直接签发这些ACME的泛域名证书吗？

Github开源项目ACME-Web-Browser-Client告诉了我们这并非是一件不可能实现的事情。

简介：

本网页客户端（仅一个静态HTML网页文件）用于：向 Let's Encrypt、ZeroSSL、Google 等支持 ACME 协议的证书颁发机构，免费申请获得用于 HTTPS 的 SSL/TLS 域名证书（RSA、ECC/ECDSA），支持多域名和通配符泛域名；只需在现代浏览器上操作即可获得 PEM 格式纯文本的域名证书，不依赖操作系统环境（Windows、macOS都能用），无需下载和安装软件，无需注册登录，纯手动操作，只专注于申请获得证书这一件事，简单易用，非常适用于希望手动快捷申请获得证书的使用场景。

Github开源地址：[https://github.com/xiangyuecn/ACME-HTML-Web-Browser-Client](https://github.com/xiangyuecn/ACME-HTML-Web-Browser-Client)

Gitee开源地址：

https://gitee.com/xiangyuecn/ACME-HTML-Web-Browser-Client

## 使用

提示：可将其私有化部署到Vercel，Netlify等上，可弥补Github Pages速度的不足。

任意点击下列一个网页使用：

https://xiangyuecn.github.io/ACME-HTML-Web-Browser-Client/ACME-HTML-Web-Browser-Client.html （作者Github Pages）

https://ssl.dev.inkdust.top/ （本人Vercel）

## 签发Let's Encrypt

本文为签发Let's Encrypt篇教程，签发ZeroSSL或Google，请看ZeroSSL篇和Google篇。

### 步骤一：选择证书颁发机构

在“证书颁发机构 ACME(v2, RFC 8555) 服务URL”下选择Let's Encrypt，点击 `读取服务目录`并等待出现：

读取服务目录成功，请进行下一步操作。 URL=https://acme-v02.api.letsencrypt.org/directory

即为成功选择Let's Encrypt。

### 步骤二：证书配置

提示：如果上次申请过证书，可以拖拽已下载保存的记录LOG文件到本页面，将自动填充上次的配置信息。

在“证书中要包含的域名：”中填写你要签发的域名。

泛域名填写方式：example.com,*.example.com

单域名填写方式：www.example.com

多域名合并：www.example.com,site1.example.com,site2.example.com

`带通配符的域名只支持DNS验证，其他域名支持上传文件验证`

在 `证书的私钥：`处一般选择 `创建新RSA私钥`或 `创建新ECC私钥`，根据证书的加密形式而定。

在 `ACME账户的私钥：`处一般选择 `创建新RSA私钥 `或 `创建新ECC私钥 `，根据证书的加密形式而定。

在 ` ACME账户的联系邮箱：`处填写你的邮箱，该邮箱必须真实存在。

### 步骤三：验证域名所有权

请给每个域名选择一个你合适的验证方式，泛域名只能使用DNS解析方式。

DNS解析方式：登陆到你的解析提供平台，如DNSPod，CloudFlare等，添加一条或多条TXT记录。

文件验证方式：仅限单域名，在你域名所属的文件目录下 创建 `/.well-known/acme-challenge/`目录并在内创建验证文件。

TLS-ALPN-01：使用Key Authorizations (Token+.+指纹)自行处理，Digest为Key Authorizations的SHA-256 Base64值。

完成后，点击“开始验证”即可验证。

## 步骤四：下载保存证书PEM文件

完成验证后，服务端会自动签发SSL证书，点击下载即可下载证书对应私钥，公钥和Log文件。

### 其他提示

1.你需要其他格式的证书文件？

大部分服务器程序支持直接使用 your_domain.pem+your_domain.key 来配置开启HTTPS（比如Nginx），如果你需要 *.pfx、*.p12 格式的证书（比如用于IIS），请用下面命令将PEM证书转换成 pfx/p12 格式：

```shell
openssl pkcs12 -export -out your_domain.pfx -inkey your_domain.key -in your_domain.pem
```

2.IIS证书链缺失？

对于Windows IIS服务器，你需要将证书链安装到“本地计算机”的“中间证书颁发机构”中；请将PEM证书中的所有证书拆分成单个PEM文件（后缀改成.crt或.cer），然后将系统中缺失的中间证书双击打开然后安装进去；详细参考： http://support.microsoft.com/kb/954755
