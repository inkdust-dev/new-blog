---
abbrlink: ''
categories:
- - 技术教程
index_img: https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/blog-image/wordpress-high-speed.png
date: '2023-08-08T18:55:35.536284+08:00'
tags:
- WordPress
- 加速
title: WordPress高速加载性能优化方案
updated: '2024-08-07T22:31:49.591+08:00'
---
从七个个角度优化你的个人/商务WordPress博客。

# 选用层

## 服务器选用

若你想在中国大陆地区获得良好的速度优化，建议你购买国内服务器并完成 `网站备案`后，再开始部署你的WordPress博客程序。

腾讯云网站备案指南：[网站备案 如何快速备案您的网站-快速入门-文档中心-腾讯云 (tencent.com)](https://cloud.tencent.com/document/product/243/39038)

阿里云网站备案指南：[操作指南\_备案-阿里云帮助中心 (aliyun.com)](https://help.aliyun.com/zh/icp-filing/user-guide/?spm=a2c4g.11186623.0.0.38a81d9cGvrtAA)

百度云网站备案指南：[ICP备案服务-百度智能云 (baidu.com)](https://cloud.baidu.com/doc/BeiAn/index.html)

网易云网站备案指南；[首次备案教程\_域名与备案\_产品文档\_帮助与文档-网易数帆 (163.com)](https://sf.163.com/help/documents/190221998684819456)

七牛云网站备案指南：[首次备案指南\_使用指南\_云主机 - 七牛开发者中心 (qiniu.com)](https://developer.qiniu.com/qvm/4184/qvm-first-guide)

工业和信息化部政务服务平台（ICP/IP地址/域名信息备案管理系统）：[ICP/IP地址/域名信息备案管理系统 (miit.gov.cn)](https://beian.miit.gov.cn/#/Integrated/index)

腾讯云轻量应用服务器购买（无AFF）：[轻量应用服务器Lighthouse\_香港轻量服务器\_海外轻量服务器-腾讯云 (tencent.com)](https://cloud.tencent.com/product/lighthouse)

腾讯云CVM云服务器购买（无AFF）：[云服务器CVM\_云主机\_云计算服务器\_弹性云服务器-腾讯云 (tencent.com)](https://cloud.tencent.com/product/cvm)

腾讯云GPU服务器购买（无AFF）：[GPU云服务器\_并行计算\_弹性计算\_人工智能\_深度学习-腾讯云 (tencent.com)](https://cloud.tencent.com/product/gpu)

阿里云轻量应用服务器购买（无AFF）：[轻量应用服务器\_web服务器\_个人建站\_弹性计算-阿里云 (aliyun.com)](https://www.aliyun.com/product/swas?spm=5176.28055625.J_3207526240.20.5421154aQbMvxH&scm=20140722.S_function@@product@@65233._.ID_function@@product@@65233-RL_%E8%BD%BB%E9%87%8F-LOC_bar-OR_ser-V_3-P0_0)

阿里云ECS云服务器购买（无AFF）：[云服务器ECS\_云主机\_服务器托管\_弹性计算-阿里云 (aliyun.com)](https://www.aliyun.com/product/ecs?spm=5176.21213303.744563.1.cb5153c90W1CYv&scm=20140722.S_card@@%E4%BA%A7%E5%93%81@@163972.S_card0.ID_card@@%E4%BA%A7%E5%93%81@@163972-RL_%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20ECS-OR_ser-V_3-P0_0)

百度云轻量应用服务器LS购买（无AFF）：[轻量应用服务器 LS\_web服务器\_小规格云服务器-百度智能云 (baidu.com)](https://cloud.baidu.com/product/lightserver.html)

百度云云服务器BCC购买（无AFF）：[轻量应用服务器 LS\_web服务器\_小规格云服务器-百度智能云 (baidu.com)](https://cloud.baidu.com/product/lightserver.html)

其他IDC云服务商的服务器暂不列出。

若你想在中国大陆地区获得良好的速度优化，且不想进行繁杂的网站备案，建议选择亚洲地区的云服务器/ECS/轻量应用服务器/VPS，此处不再列举。

若你不想在中国大陆地区获得良好的速度优化，请关闭这篇文章。

## CDN选用

良好的CDN不仅可以为网站提速，还可以隐藏源站IP地址，保护服务器不受恶意攻击。

关于CDN的选用，可以在各大搜索引擎上搜索到，国内已备案建议选择国内CDN，未备案则只能选择国外CDN。

我个人常用的几个CDN提供商：

腾讯云：[CDN 内容分发网络 \_CDN内容加速\_CDN加速-腾讯云 (tencent.com)](https://cloud.tencent.com/product/cdn)

阿里云：[CDN\_内容分发网络\_CDN网站加速-阿里云 (aliyun.com)](https://www.aliyun.com/product/cdn?spm=5176.28055625.J_3207526240.50.5421154a9V4vEf&scm=20140722.S_function@@product@@96099._.ID_function@@product@@96099-RL_cdn-LOC_bar-OR_ser-V_3-P0_0)

初七云：[购物车 - 初七云 - 企业级云服务器、高防服务器、香港服务器、免费CDN云计算服务商！ (chuqiyun.com)](https://chuqiyun.com/cart?fid=2&gid=3)

CloudFlare：[Cloudflare 中国官网 | 智能化云服务平台 | 免费CDN安全防护 | Cloudflare (cloudflare-cn.com)](https://www.cloudflare-cn.com/)

CacheFly：[Trusted CDN Provider | Faster Content Delivery | CacheFly](https://www.cachefly.com/)

Gcore：[Gcore | 全球托管、CDN、边缘和云服务](https://gcore.com/zh)

## 主题选用

尽量选择图片加载量较少的，JS较少的主题，可以显著提升加载速度。这里不列举。

# 加速层

## JS/CSS/图片静态文件加速

建议选用WP-Rocket和对象存储+CDN的方式，对CDN路径进行映射，如果没有钱购买WP-Rocket，可以通过WPJAM实现同样的效果。

对象存储配置（原文地址：[WPJAM Basic 详细介绍：一键实现 WordPress 静态资源 CDN 加速 - WordPress 果酱](https://blog.wpjam.com/m/wpjam-basic-cdn/)）：

* [WordPress 博客使用阿里云对象存储 OSS 进行静态资源 CDN 加速](https://blog.wpjam.com/m/aliyun-oss-cdn/)
* [WordPress 博客使用腾讯云对象存储 COS 进行静态资源 CDN 加速](https://blog.wpjam.com/m/qcloud-cos-cdn/)
* [WordPress 博客使用火山引擎 veImageX 进行静态资源 CDN 加速](https://blog.wpjam.com/m/volc-veimagex/)

然后就可以使用WP-Rocket映射CDN CNAME：

在 `WP Rocket`插件设置中，在CDN选项里，启用CDN，并在CDN CNAME中填入配置好的CDN域名，并选中套用到所有文件，如下图：

![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/2023/8/8-768x342_ae4f2f18235ab0d5ded34c124275f9d3.jpg](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/2023/8/8-768x342_ae4f2f18235ab0d5ded34c124275f9d3.jpg)

或者在WPJAM中设置：

![wpjam](https://cdn.97866.com/wp-content/uploads/sites/26/2023/05/1684249708-image.png?imageMogr2/auto-orient/thumbnail/!1200x722r/gravity/Center/crop/1200x722/quality/70/interlace/1|watermark/1/image/aHR0cHM6Ly9jZG4ud3BqYW0uY29tL3dwamFtL3dhdGVybWFyay5wbmc/dissolve/50#)

设置完成后即可享受快速的CSS/JS/图片加速。

WPJAM下载链接：[WPJAM Basic – WordPress 插件 | WordPress.org China 简体中文](https://cn.wordpress.org/plugins/wpjam-basic/)

WP-Rocket开心版下载：[wp-rocket\_v3.14.1.zip - Cloudreve (awak.top)](https://pan.awak.top/s/k5h6)

## 头像/字体/后台加速

说到后台核心文件加速，我想到了使用WP-China-Yes，但其对谷歌字体的加速已失效，我将其修改到了Google官方的CN镜像地址，同时将Gravatar替换为我自建的SDN地址（FallSoft SDN）。

![https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/2023/8/20230808195915_3bd36a8fd66f78a5ce2033d9ad5407f1.png](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/qexo-upload/2023/8/20230808195915_3bd36a8fd66f78a5ce2033d9ad5407f1.png)

WP-China-Yes自用修改版：[wp-china-yes.zip - Cloudreve (awak.top)](https://pan.awak.top/s/l5i5)

## Opcache

宝塔：在宝塔面板中安装PHP扩展Opache即可。

Oneinstack：`./install.sh --php_extensions opcache`

LNMP：[LNMP安装php扩展模块（eAccelerator、xCache、memcached、imageMagick和ionCube） (biancheng.net)](http://c.biancheng.net/view/1135.html)

## Redis/Memcached

### Redis

安装Redis：[Linux安装部署Redis(超级详细) - 长沙大鹏 - 博客园 (cnblogs.com)](https://www.cnblogs.com/hunanzp/p/12304622.html)

宝塔面板直接在软件商店安装Redis即可。(无需设置)

安装[Redis Object Cache – WordPress 插件](https://cn.wordpress.org/plugins/redis-cache/)。

开启插件后会自动连接到Redis。

### Memcached

本人不熟悉，指路：

[使用 Memcached 内存缓存来提高 WordPress 站点速度 - WordPress 果酱 (wpjam.com)](https://blog.wpjam.com/article/wordpress-memcached/)

[Cache | Screen-by-Screen | LSCache for WordPress | LiteSpeed Documentation (litespeedtech.com)](https://docs.litespeedtech.com/lscache/lscwp/cache/#object-tab)

## Service Worker

参考自：[为WordPress启用Service Worker | 青空之蓝 (ixk.me)](https://blog.ixk.me/post/wordpress-enabled-service-worker)

### 加入 sw-toolbox 核心至 WordPress

下载[sw-toolbox.js](https://cdnn.boochi.cn/gh/inkdust-dev/ink-oss@main/js/sw-toolbox.js)并且放到博客程序的根目录.

### 创建缓存规则

在博客个目录创建一个serviceworker.js，根据网站情况书写，下面是[GalX次元 - 免费的galgame资源站 (galxfans.top)](https://www.galxfans.top/)的Service Worker规则示例：

```javascript
"use strict";

(function () {
  "use strict";
  /**
   * Service Worker Toolbox caching
   */

  var cacheVersion = "-toolbox-v1";
  var dynamicVendorCacheName = "dynamic-vendor" + cacheVersion;
  var staticVendorCacheName = "static-vendor" + cacheVersion;
  var staticAssetsCacheName = "static-assets" + cacheVersion;
  var contentCacheName = "content" + cacheVersion;
  var maxEntries = 50;
  //以下的网址请更换为博客地址(可以填写绝对链接或者相对链接)
  self.importScripts("https://www.galxfans.top/sw-toolbox.js");
  self.toolbox.options.debug = false;
  //由于我的博客启用Autoptimize，以及WP Super Cache，所以添加Cache目录
//   self.toolbox.router.get("wp-content/cache/(.*)", self.toolbox.cacheFirst, {
//     cache: {
//       name: staticAssetsCacheName,
//       maxEntries: maxEntries
//     }
//   });
  //添加毒瘤jquery的缓存规则
  self.toolbox.router.get(
    "wp-includes/js/jquery/jquery.js",
    self.toolbox.cacheFirst,
    {
      cache: {
        name: staticAssetsCacheName,
        maxEntries: maxEntries
      }
    }
  );
  //添加主题的静态资源，具体目录请自行更换
  self.toolbox.router.get(
    "wp-content/themes/Autumn-Pro/static/(.*)",
    self.toolbox.cacheFirst,
    {
      cache: {
        name: staticAssetsCacheName,
        maxEntries: maxEntries
      }
    }
  );
  self.toolbox.router.get(
    "wp-includes/css/(.*)",
    self.toolbox.cacheFirst,
    {
      cache: {
        name: staticAssetsCacheName,
        maxEntries: maxEntries
      }
    }
  );
  //以下均为第三方资源缓存
  self.toolbox.router.get("/(.*)", self.toolbox.cacheFirst, {
    origin: /cdn2\.chuqis\.com/,
    cache: {
      name: staticVendorCacheName,
      maxEntries: maxEntries
    }
  });

  self.toolbox.router.get("/(.*)", self.toolbox.cacheFirst, {
    origin: /cdn\.chuqis\.com/,
    cache: {
      name: staticVendorCacheName,
      maxEntries: maxEntries
    }
  });

  // 缓存 cdn
  self.toolbox.router.get("/(.*)", self.toolbox.fastest, {
    origin: /cdn\.staticfile\.org/,
    cache: {
      name: staticVendorCacheName,
      maxEntries: maxEntries
    }
  });

  self.toolbox.router.get("/(.*)", self.toolbox.fastest, {
    origin: /cravatar\.cn/,
    cache: {
      name: staticVendorCacheName,
      maxEntries: maxEntries
    }
  });
  
  self.toolbox.router.get("/(.*)", self.toolbox.fastest, {
    origin: /unpkg\.com/,
    cache: {
      name: staticVendorCacheName,
      maxEntries: maxEntries
    }
  });
  self.toolbox.router.get("/(.*)", self.toolbox.fastest, {
    origin: /img\.galx\.umine\.top/,
    cache: {
      name: staticVendorCacheName,
      maxEntries: maxEntries
    }
  });
  self.toolbox.router.get("/(.*)", self.toolbox.fastest, {
    origin: /inkdustv\.cachefly\.net/,
    cache: {
      name: staticVendorCacheName,
      maxEntries: maxEntries
    }
  });


//   self.toolbox.router.get("/(.*)", self.toolbox.cacheFirst, {
//     origin: /(fonts-gstatic\.yecdn\.com|www\.google-analytics\.com)/,
//     cache: {
//       name: staticVendorCacheName,
//       maxEntries: maxEntries
//     }
//   });

  // immediately activate this serviceworker
  self.addEventListener("install", function (event) {
    return event.waitUntil(self.skipWaiting());
  });

  self.addEventListener("activate", function (event) {
    return event.waitUntil(self.clients.claim());
  });
})();

```

### 启用 Service Workers

打开主题文件所在目录，修改 footer.php，在 `</body>` 前加入以下代码:

```javascript
<script>
  var serviceWorkerUri = "/serviceworker.js";

  if ("serviceWorker" in navigator) {
    navigator.serviceWorker
      .register(serviceWorkerUri)
      .then(function () {
        if (navigator.serviceWorker.controller) {
          console.log("Assets cached by the controlling service worker.");
        } else {
          console.log(
            "Please reload this page to allow the service worker to handle network operations."
          );
        }
      })
      .catch(function (error) {
        console.log("ERROR: " + error);
      });
  } else {
    console.log("Service workers are not supported in the current browser.");
  }
</script>

```

即刻享受Service Worker毫秒级响应加速。

更多加速方法，请自行探索！
