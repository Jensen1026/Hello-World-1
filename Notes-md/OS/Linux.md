# Linux notes
[TOC]

## Linux Desktop

## Linux Server

### 远程连接服务器

#### SSH

##### autologin

###### lightdm (xfce)

```
[SeatDefaults]
autologin-user=username	#需要登录的用户名
autologin-user-timeout=delay
```
##### 不显示grub引导菜单

```bash
vim /etc/default/grub
update-grub
```

##### 修改欢迎介面

* /etc/issue
* /etc/issue.net
* /etc/motd

### Apt

* [apt官方wiki](https://wiki.debian.org/Apt)

