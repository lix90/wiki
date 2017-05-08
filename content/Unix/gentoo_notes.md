---
title: "Gentoo Notes"
author: lixiang
date: 2017-05-07 13:13
tag: gentoo,linux
---

# Install Gentoo **TODO**

# 系统配置

桌面：X11, XFCE, awesome
字体：wqy-microhei, source-pro, source-han-sans, droid, noto-cjk, arphicfonts, opendesktop-fonts
其他：xmodmap, layman, overlay, eix

# 安装常用软件

开发与数据分析：nodejs, anaconda, R, RStudio, zsh, oh-my-zsh
输入法：fcitx
版本控制：Git
浏览器：Chrome
编辑器：Emacs, Vim, Sublime Text 3
网络：shadowsocks-libev, proxychains-ng, axel
娱乐：youtube-dl, smplayer
图像编辑处理：inkscape, gimp
办公：okular, libreoffice, calibre, zotero, evince

# 主题配置

## arc-theme

实现主题的窗口部分无法识别出来。后来发现是少了use 标签，加上我所使用的桌面应用xfce之后成功加载了窗口主题。

## [papirus-icon-theme](https://github.com/PapirusDevelopmentTeam/papirus-icon-theme)

``` shell
wget -qO- https://raw.githubusercontent.com/PapirusDevelopmentTeam/papirus-icon-theme/master/install-papirus-home-gtk.sh | sh
```

# 问题解决

## 无法调用出fcitx中文输入法

使用 `fcitx-diagnose` 进行诊断，将报错标红的依赖包给加入use flags。

# Gentoo基本知识

## 内核

## 包管理

## 配置

emerge
eselect
