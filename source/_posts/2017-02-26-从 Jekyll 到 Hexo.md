---
layout: post
title: 从 Jekyll 到 Hexo
comments: true
---

之前这个博客一直用 [Jekyll][3]，虽然 Jekyll 挺方便，但是除了 Jekyll，几乎没有能用到 Ruby 的地方。在折腾的过程中感觉 Ruby 对 Windows 的支持极差，虽然能用但总归不爽。再者自己用的最多的就是 JavaScript 与 Node.js，叛逃到 [Hexo][5] 应该是迟早的事。去年折腾过 Hexo，应该是部署过程中有坑，然后就没管它，那时候嫌麻烦吧。昨天给 [eggjs][4] 修改文档，刚好手头是 Windows 然后 eggjs 的文档又用了 Hexo，随即尝试了一下，竟然跑起来了。改完文档以后，就果断把自己的博客迁移到了 Hexo。

迁移过程中，发现大致要注意一下几个点吧：
 * 配置 [github ssh key][1] (解决自动部署没有权限的问题)
 * 指定合适的部署 branch，我指定的是 gh-pages (因为 Hexo 会默认把其它不是从 source 目录上生成的内容在提交时干掉)，然后用master保存其它没有提交的内容。
 * 给 git 加个[代理][2]，你会发现 github 还是能用的 

[1]: https://help.github.com/articles/connecting-to-github-with-ssh/
[2]: https://gist.github.com/laispace/666dd7b27e9116faece6
[3]: https://jekyllrb.com/
[4]: https://eggjs.org/
[5]: https://hexo.io/zh-cn/