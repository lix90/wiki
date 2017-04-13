---
title: "Miscellaneous"
author: Lixiang
date: 2017-03-18 17:58:35
tag: tool
description: "备忘录杂项"
---

**Babun** 一个不错的 Windows 系统下的 shell，因为换到 MacOS，所以还没用过
**unsplash** 一个免费的高清图库
**WebSlides** 一个演示文稿框架
**Matterwiki** wiki平台
**Skytorrent.in** 种子搜索引擎

**oh-my-zsh** 一个管理 zsh 配置的框架
**autoconfig-mac-vimrc** 一个前端的vim配置
**ielm** interactive emacs lisp mode

---

# socks5 转 http 代理

需要为calibre设置代理抓取不能直接抓取的新闻源。但是calibre只支持http代理。故希望将socks5转http。使用privocy可以将socks5代理转为http代理。

```
brew install privoxy
```

配置privacy `/usr/local/etc/privoxy/config`。

末尾添加

```
listen-address 0.0.0.0:1081
forward-socks5 / 127.0.0.1:1080
```
