---
abbrlink: ''
categories: []
index_img: https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/blog-image/vercel-recover.png
date: '2023-10-04T15:00:38.639280+08:00'
tags: []
title: '[2023.10]Vercel国内阻断解决方案'
updated: '2024-08-07T22:32:23.792+08:00'
---
## 简单操作

将Vercel的CNAME更换成 `vercel.dns.inkdust.top`，可快速解决无法访问的情况，等待DNS刷新后即可访问到网站。

## 自选IP

在下面的IP列表中选择合适的Vercel IP地址（IP地址由ChenYFan提供），并自定义解析路线。
[https://gist.github.com/ChenYFan/fc2bd4ec1795766f2613b52ba123c0f8#file-ip-txt-L3](https://gist.github.com/ChenYFan/fc2bd4ec1795766f2613b52ba123c0f8#file-ip-txt-L3)
如果不能打开，请看下方代码块：

```
34.95.57.145 [加拿大 魁北克省蒙特利尔 Google 云计算数据中心]
13.49.54.242 [瑞典 斯德哥尔摩 Amazon 数据中心]
18.178.194.147 [日本 东京都东京 Amazon 数据中心]
52.79.72.148 [韩国 首尔 Amazon 数据中心]
35.180.16.12 [法国 巴黎 Amazon 数据中心]
18.206.69.11 [美国 弗吉尼亚州阿什本 Amazon 数据中心]
52.76.85.65 [新加坡 Amazon 数据中心]
18.130.52.74 [英国 伦敦 Amazon 数据中心]
35.202.100.12 [美国 Merit 网络公司]
35.195.188.93 [比利时 瓦隆大区圣吉斯兰 Google 云计算数据中心]
3.22.103.24 [美国 Amazon EC2 服务器]
34.253.160.225 [爱尔兰 都柏林 Amazon 数据中心]
18.229.231.184 [巴西]
15.206.54.182 [美国 惠普 HP]
35.235.101.253 [美国 加利福尼亚州洛杉矶 Google 云计算数据中心]
35.196.196.42 [美国 Merit 网络公司]
35.228.53.122 [美国 俄勒冈州达尔斯 Google 云计算数据中心]
34.65.228.161 [美国 得克萨斯州]
52.38.79.87 [美国 俄勒冈州波特兰 Amazon 数据中心]
13.238.105.1 [澳大利亚 新南威尔士州悉尼 Amazon 数据中心]
104.199.217.228 [台湾省彰化县 Google 云计算数据中心]
52.9.164.177 [美国 加利福尼亚州旧金山 Amazon 数据中心]
18.162.37.140 [香港 Amazon 数据中心]
```

可自行选择合适的IP解析，或在IP失效时更换其他IP。

## 更换构建程序

例如：Azure Static App、Aws Amplify、Netlify、CloudFlare Page/S3、4everland等，可在网上自行查询。
