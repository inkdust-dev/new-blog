---
abbrlink: ''
categories:
- - 技术教程
- - 免费资源
index_img: https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/blog-image/cloudflare-saas.png
date: '2023-07-16 19:06:46'
tags:
- Cloudflare
- 免费CDN
- CNAME接入
title: CloudFlare官方免费CNAME接入及自选IP教程
updated: '2024-08-07T22:33:20.763+08:00'
---
自2021年年末后，Cloudflare禁用了使用 `API_KEY`自定义CNAME接入 `Partner`的方式，自选节点IP成为了历史。

真的没有办法自选IP了

吗?

当然是有的，而且是Cloudflare官方提供的CNAME接入，即 `Cloudflare for SaaS`，我们依旧可以通过该方式来自定义IP节点，并且共享页面规则和WAF防火墙规则。

## 什么是CloudFlare SaaS

CloudFlare SaaS是指CloudFlare提供的基于云计算的软件即服务（Software-as-a-Service）解决方案。CloudFlare是一家提供网络安全和性能优化服务的公司，其SaaS产品能够帮助企业提高网站的安全性、可靠性和性能。使用CloudFlare SaaS，用户无需购买、安装或管理软件，而是通过互联网访问CloudFlare的平台，在云端享受各种功能和服务。这些服务包括DDoS保护、网站加速、负载均衡、SSL证书管理、全球内容分发网络（CDN）等。通过CloudFlare SaaS，用户可以轻松改善其在线应用程序和网站的用户体验，并减轻自身的技术负担。
（回答来自ChatGPT）

## 准备工作

俗话说:“工欲善其事，必先利其器”，我们需要提前准备好以下材料：以及

- 域名 两个(允许免费的Freenom域名)
- CloudFlare 账户 一枚
- 一个支持分线解析的DNS解析平台账号
- 外币信用卡(允许0额度卡和虚拟信用卡) 一张 `(不收取任何费用)`

或者

- Paypal账号一个

## CloudFlare 操作篇

1.打开 `CloudFlare官网`，登录/注册账号，添加好你的网站域名并修改 `NameServer`使其在Cloudflare保持 `Active`状态。(注意:该域名并不是你访问的域名，而是你通过CNAME接入的地址，所以，你可以直接放心大胆的使用 `Freenom`域名!

![CloudFlare接入域名](https://cdnn.boochi.cngh/inkdust-dev/ink-oss/main/image/20230711193423.png?image_process=format,webp "如图，已成功接入域名")

接入完成后我们直接打开账户的 `付款方式`，点击 `用户头像`，点击 `账单`-`付款信息`，在此添加Paypal或信用卡。

接着订购 `CloudFlare for SaaS`，进入你的域名，按下图所示操作订购服务，可以看到100个域名的免费额度。

![购买SaaS](https://cdnn.boochi.cngh/inkdust-dev/ink-oss/main/image/20230711193833.png?image_process=format,webp)

接下来，就是确定源站了。

添加一个DNS记录，可以是任何记录(A,CNAME,…)。记录名建议为 `origin`，然后在自定义主机名页面中添加 `origin.<YOUR_DOMAIN>`，在底下添加你的访问域名，例如 `www.example.com`。

![添加回退源](https://cdnn.boochi.cngh/inkdust-dev/ink-oss/main/image/20230711194134.png?image_process=format,webp)
![SaaS设置](https://cdnn.boochi.cngh/inkdust-dev/ink-oss/main/image/20230711194134.png?image_process=format,webp)

至此，你已完成了CloudFlare的操作。

## 分线解析DNS 操作

登录支持分线解析的DNS控制台，这里以 `DNSPOD`为例，添加你的域名，并修改 `NameServer`，使其变为 `正常解析`状态。

添加一个CNAME解析到 `origin.<YOUR_DOMAIN>`，然后添加Cloudflare证书需要添加的记录。

![添加证书记录](https://alpha-q3.sourcegcdn.com/2022/08/05/OGUDjNmj.jpg/webp)

如有记录冲突请自行暂停和删除部分解析。

待证书状态变为有效后就可以自选IP了。

例如将 `www.example.com`的电信运营商解析到 `1.1.1.1`，就可以添加电信运营商的A记录到 `1.1.1.1`。

![添加最佳IP](https://cdnn.boochi.cngh/inkdust-dev/ink-oss/main/image/20230711195117.png?image_process=format,webp)

然后，访问你的域名，如果能访问的话，恭喜你成功接入。

## 自选IP工具

([XIU2/CloudFlare Speed Test])[https://github.com/XIU2/CloudflareSpeedTest]

## 最后

CloudFlare的节点数目众多，但资源有限，请勿滥用。
