# Deepin Linux

## 分区方案

```text
/boot/efi   vfat    300M

/boot   ext4    5G

/   ext4    50G

/home   ext4    剩余所有
```

## 基本设置

### Grub
*推荐手动在设置里面修改*

```bash
#开机不显示grub引导菜单
sudo sed -i 's/^GRUB_TIMEOUT=./GRUB_TIMEOUT=0/' /etc/default/grub && update-grub
```
#### grub 主题

[Grub Themes](https://www.gnome-look.org/browse/cat/109/ord/rating/)

### 关闭蜂鸣提示音

*Deepin已经不需要*

#### 单用户设置
```bash
echo set bell-style none >> ~/.inputrc

echo xset -b >> ~/.zshrc
```

#### 全局设置

```bash
#编辑 /etc/inputrc 文件
vim /etc/inputrc

#找到 #set bell-style none 这行，删除前面的注释符号
```

### 显卡驱动

```bash
sudo apt-get install nvidia-driver

#使用英伟达闭源驱动
```

## 深度终端

* 远程命令
  >sudo apt-get install lrzsz

  >安装 rz 和 sz 命令

* 终端字体
  >SauceCodePro Nerd Font Mono
  >13

* 终端主题
  >one dark

### tmux

### rangers

### irssi

#### 频道

* \#emacs
* \##ustc_lug
* \#linuxdeepin

### Editor

* emacs
* vim
* vscode

### Hack Tools

* tcpdump
* wireshark
* nmap

## 办公

* 百度网盘 for Linux

## Development Envirnoment

* Lisp
  * sbcl

* C
  * gcc
  * gdb
  * clang

* golang
  * how to install
    >sudo apt-get install golang

* cmake

## Deepin 开发指南

[博客](https://deepin.lolimay.cn/)

[Github](https://github.com/loliMay/deepin-develop-guide)
