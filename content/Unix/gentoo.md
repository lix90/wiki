---
title: "Gentoo Notes"
author: lixiang
date: 2017-05-09 13:29
tag: gentoo,linux
---

# 字体

mplus-spa

手动安装字体

``` shell
cp <font filename> /usr/share/fonts/
# 建立字体索引信息，更新字体缓存
cd /usr/share/fonts/
mkfontscale
mkfontdir
fc-cache
```

显示默认字体

``` shell
fc-match "sans"
fc-match "serif"
fc-match "mono"
```

显示已安装中文字体

``` shell
fc-list :lang=zh
```

# add gentoo-zh overlay

gentoo-china-overlay & gentoo-taiwan-overlay已经合并成 gentoo-zh

``` shell
sudo emerge -avt layman
sudo layman -L
sudo layman -a gentoo-zh
```

# use eix

# 查看内核编译配置

``` shell
zcat /proc/config.gz
cat /boot/config-`uname -r`
```

# 编译内核

``` shell
cd /usr/src/linux
cp .config /config-`uname -r` ## back up kernel config

make menuconfig

make && make modules_install
make install ## copy kernel image to /boot
```

# 挂载ntfs移动硬盘

1. 配置内核

    > File systems  —>
    >   DOS/FAT/NT Filesystems  —>
    >     <*> NTFS file system support
    >     [ ]   NTFS debugging support
    >     [*]   NTFS write support
    >
    >   <*> Filesystem in Userspace support

2. 编译ntfs-3g

``` shell
emerge ntfs3g
```

3. 挂载

``` shell
mkdir ~/hd
sudo mount -t ntfs-3g /dev/sd* ~/hd
```

# tty console

> 使用文字介面的時候，會看到tty1、tty2之類的名稱，這是什麼東西呢？TTY是「Teletypes」這個字的縮寫，原意是打字機，引申為打字輸入的介面，也就是終端機(Terminal)的文字輸入介面。tty之後接的號碼，可以想像成是第幾台終端機，例如tty1就是第一台終端機。Linux預設有七台終端機，分別是tty1、tty2、tty3、tty4、tty5、tty6、tty7，tty7一般作為X-Window圖形介面使用。切換不同tty的方式很簡單，只要使用鍵盤組合鍵即可達成，按法為：「ctrl + alt + F1~F7」，「F」的號碼就代表tty的號碼。如按下「ctrl + alt + F5」就可以切換到tty5。[link](https://magiclen.org/linux-text/)

`Ctrl+Alt+F1-F6`
`Ctrl+Alt+F7` 返回图形界面

# 触控板配置

个人使用xfce, 自带设置界面, 基本满足要求.

# 配置texlive2016

set repository

``` shell
tlmgr option repository http://mirrors.aliyun.com/CTAN/systems/texlive/tlnet/
```

# 配置xfce

``` shell
sudo emerge -avt thunar-vcs-plugin xfce4-clipman-plugin xfce4-composite-editor xfce4-cpufreq-plugin xfce4-cpugraph-plugin xfce4-datetime-plugin xfce4-diskperf-plugin xfce4-indicator-plugin xfce4-kbdleds-plugin xfce4-linelight-plugin xfce4-mailwatch-plugin xfce4-mixer xfce4-netload-plugin xfce4-netspeed-plugin xfce4-notes-plugin xfce4-notifyd xfce4-places-plugin xfce4-playercontrol-plugin xfce4-pulseaudio-plugin xfce4-screenshooter xfce4-systemload-plugin xfce4-time-out-plugin xfce4-timer-plugin xfce4-vala xfce4-volumed xfce4-wavelan-plugin xfce4-whiskermenu-plugin xfce4-windowck-plugin xfce4-xkb-plugin
```

# 安装pandoc

# 配置网络

## NetworkManager

networkmanager不能与其他网络管理服务同时工作。确保同时只能运行一个网络管理服务。

``` shell
rc-service NetworkManager start
rc-update add NetworkManager default
```

nmcli

列出wifi列表：`nmcli dev wifi`
连接wifi：`nmcli dev wifi connect <name> password <password>`
断开wifi：`nmcli dev disconnect wifi`

## 获取网络设备信息

获取基本信息（bus-id, manufacturer, model）：`lspci | grep -i net`
硬件信息：`lshw -class network`
硬件与配置信息：`inxi -N -v 7`
网络配置：`ip ad show`


## 配置无线wifi

检测wifi驱动：lspci或者lsusb

``` shell
sudo lspci -k
...
03:00.0 Network controller: Realtek Semiconductor Co., Ltd. RTL8192EE PCIe Wireless Network Adapter
    Subsystem: Realtek Semiconductor Co., Ltd. RTL8192EE PCIe Wireless Network Adapter
```

[Fixing the Realtek rtl8192ee driver on Linux](http://damienfirmenich.com/2015/04/12/t450s-rtl8191ee.html)
[Network Manager](https://wiki.gentoo.org/wiki/NetworkManager)

``` shell
git clone https://github.com/lwfinger/rtlwifi_new

cd rtlwifi_new
make

sudo make install

## reboot
## sudo modprobe rtl8192ee

## repeat after every kernel update
echo "options rtl8192ee swenc=1" > /etc/modprobe.d/rtl8192ee.conf
sudo rmmod rtl8192ee
sudo modprobe rtl8192ee
```

安装rtfwifi_new时保存

``` shell
lexiangli@gentoo ~/Documents/gh_repos/rtlwifi_new $ sudo make install
Password: 
make -C /lib/modules/4.9.16-gentoo/build M=/home/alexiangli/Documents/gh_repos/rtlwifi_new modules
make[1]: Entering directory '/usr/src/linux-4.9.16-gentoo'
  Building modules, stage 2.
  MODPOST 15 modules
make[1]: Leaving directory '/usr/src/linux-4.9.16-gentoo'
Making backups
tar: /lib/modules/4.9.16-gentoo/kernel/drivers/net/wireless/rtlwifi: Cannot stat: No such file or directory
tar: Exiting with failure status due to previous errors
make: *** [Makefile:62: install] Error 2
```

解决：新建报错中的路径 `sudo mkdir <directory> -p`, 然后继续执行 `sudo make install`

# Add startup service

# 配置声卡

配置内核
将alsa加入全局USE: `euse -E alsa`
安装 `emerge -avt alsa-utils`
保证用户在audio用户组中
开启alsa服务
开机启动
调节音量工具alsamixer
测试声音 `speaker-test -t wav -c 2`


# launcher

albert `emerge -avt albert`
synapse `emerge -avt synapse`

# 格式化U盘

format USB disk into fat32

``` shell
sudo fdisk -l
# fdisk /dev/sd*
# make new partition of fat32 type
emerge -avt dosfstools
# echo 'export PATH="/usr/sbin:$PATH" >> .bashrc'
sudo mkfs.vfat -n "name" /dev/sd*
```

# copy with progress bar

1. `pv *** > ***`
2. `rsync -ah progress source-file destination`

# Cannot switch fcitx to chinese input mode in Konsole

`sudo emerge -avt fcitx-qt5`

# fx sublime-text-3 chinese input via fcitx

git clone [sublime-text-imfix](https://github.com/lyfeyaj/sublime-text-imfix)

``` shell
git clone https://github.com/lyfeyaj/sublime-text-imfix
cd sublime-text-imfix && ./sublime-imfix
# unmerge sublime-text
# remerge sublime-text
```

# 工具软件

命令行词典

* sdcv: `emerge sdcv`
* ici: `pip install ici`
* ydcv
* iSearch

# 窗口管理

x11-wm/awesome

1. 安装awesome：`emerge -avt x11-wm/awesome`
2. 运行显示管理器和X时启动awesome：在 `~/.xinitrc`添加 `exec ck-launch-session dbus-launch --sh-syntax --exit-with-session awesome`
3. 配置文件：`~/.config/awesome/rc.lua`; 默认配置文件位于 `/etc/xdg/awesome/rc.lua`.
4. 更改默认终端：修改 `~/.config/awesome/rc.lua` 添加 `terminal="konsole"`.
5. 检查配置文件：`awesome -k`

* 标签 Tags
* 菜单 Menu
* 时间 Date
* 音量控制 Volume control
* 多媒体键
* 快捷键
# 输入法

## 无法调用出fcitx中文输入法

使用 `fcitx-diagnose` 进行诊断，将报错标红的依赖包给加入use flags。

# 用户界面

## arc-theme

实现主题的窗口部分无法识别出来。后来发现是少了use 标签，加上我所使用的桌面应用xfce之后成功加载了窗口主题。

## [papirus-icon-theme](https://github.com/PapirusDevelopmentTeam/papirus-icon-theme)

``` shell
wget -qO- https://raw.githubusercontent.com/PapirusDevelopmentTeam/papirus-icon-theme/master/install-papirus-home-gtk.sh | sh
```

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
