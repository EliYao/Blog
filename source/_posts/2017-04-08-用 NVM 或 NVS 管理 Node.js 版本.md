---
layout: post
title: 用 NVM 或 NVS 管理 Node.js 版本
comments: true
---

Node.js 升级非常频繁，当长期使用 Node.js 进行开发工作时，有必要使用一个能够灵活切换 Node.js 版本的工具。

Node.js 版本管理工具主要有两个 [NVM][1]、[NVS][2]，前者出来相对更久一点但不支持 Windows，后者跨平台，所以现在一般推荐安装后者。

关于安装步骤，根据官方教程走就好了，非常简单，Windows NVS 安装与使用需要管理员权限，同时要设置允许运行 Powershell 脚本。

安装完以后，这里有个小建议是把它们的镜像源更改到国内，不然下载速度会非常慢，还有可能下载失败。

替换镜像源的方法如下：

### NVM

```bash
$ NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node
```

### NVS

```bash
$ nvs remote taobao https://npm.taobao.org/mirrors/node/
```

然后就能愉快的切换 Node.js 版本啦。

[1]: https://github.com/creationix/nvm
[2]: https://github.com/jasongin/nvs