---
layout: post
title: 在 Windows Subsystem for Linux (WSL) 运行 Puppeteer
comments: true
---

Windows Subsystem for Linux (WSL) 是微软在 Windows 10 中带来的新功能，在 1709 这个秋季更新的版本后它也脱离了 beta，成为了正式版本。Headless Chrome 是 Google 今年发布的新功能，而 Puppeteer 则是 Headless Chrome Node API，用于 Headless 浏览器可以做的各类事情。

选择在 WSL 运行 Puppeteer，满足了 Linux 环境的需求（可以将写好的代码直接不少到 Linux 服务器上跑），且机器性能比虚拟机里启动 Linux 好的多。默认就有 Linux 环境，就懒得再折腾虚拟机了。

按照官方 [GoogleChrome/puppeteer: Headless Chrome Node API][1] 提供的资料，装好依赖后，你在 WSL 上运行代码会得到这样一个报错

```bash
 (node:483) UnhandledPromiseRejectionWarning: Unhandled promise rejection (rejection id: 1): Error: kill ESRCH 
 (node:483) [DEP0018] DeprecationWarning: Unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the Node.js process with a non-zero exit code.
```

你和我的报错不同之处大概就只有 node: 后面的进程号了。如果把代码进行异常捕捉，你会得到这样的报错

```bash
{ Error: kill ESRCH
    at Object._errnoException (util.js:1021:11)
    at process.kill (internal/process.js:180:18)
    at killChrome (/{jsfolder}/node_modules/puppeteer/lib/Launcher.js:151:21)
    at Function.launch (/{jsfolder}/node_modules/puppeteer/lib/Launcher.js:136:7)
    at <anonymous>
    at process._tickCallback (internal/process/next_tick.js:188:7) code: 'ESRCH', errno: 'ESRCH', syscall: 'kill' }
```

{jsfolder} 是你的代码目录，到了这一步其实还是很疑惑到底报了什么错。

如果你的报错也是上面提到的这个样子，那么可以根据这个 [issue][2] 来解决问题，我将步骤提取了出来：

1. 安装环境依赖

```bash
sudo apt-get install gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils wget
```

2. 调整 Puppeteer 启动传参，传入 args

```JavaScript
const puppeteer = require('puppeteer');
(async () => {
  try {
    const brower = await puppeteer.launch({args: ['--no-sandbox']});
    const page = await brower.newPage();
    await page.goto('https://example.com');
    console.log(await page.content());
    await page.screenshot({path: 'screenshot.png'});
    await brower.close();
  } catch (e) {
    console.log(e);
  }
})();
```

PS：如果是在国内的网络，代码运行时还可能会遇到下面这个报错

```Bash
Error: Failed to navigate: https://example.com
    at Page.goto (/{jsfolder}/node_modules/puppeteer/lib/Page.js:470:13)
    at <anonymous>
    at process._tickCallback (internal/process/next_tick.js:188:7)
```
解决方法是将 https://example.com 换成国内你能访问的网站，具体原因不详。

[1]: https://github.com/GoogleChrome/puppeteer
[2]: https://github.com/Googlechrome/puppeteer/issues/290