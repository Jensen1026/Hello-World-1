### OS

* Ubuntu 18.04

### SSH

#### 免密登陆



### 基本配置

#### Autologin

###### lightdm (xfce)

```
[SeatDefaults]
autologin-user=username	#需要登录的用户名
autologin-user-timeout=delay
```
###### [Gnome](https://help.gnome.org/admin/system-admin-guide/stable/login-automatic.html.en)

```bash
#Edit the /etc/gdm/custom.conf file and make sure that the [daemon] section in the file specifies the following:
#custom.conf

[daemon]
AutomaticLoginEnable=True
AutomaticLogin=username

#Replace the username with the user that you want to be automatically logged in
```

###### [Kde]()

```bash

```

#### 不显示grub引导菜单

```bash
vim /etc/default/grub
grub2-mkconfig -o /boot/grub2/grub.cfg
(update-grub 未必都能用)
```

###### 如果主机是efi主板启动

```bash
如 centos：
则修改 /etc/default/grub 后,使用 grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
再重启。

```

#### 修改 ssh 欢迎介面

* /etc/issue
* /etc/issue.net
* /etc/motd

#### 笔记本合盖子不休眠

Ubuntu 18.04 LTS 测试有效

```bash
#编辑 /etc/systemd/logind.conf

sudo vim /etc/systemd/logind.conf
#去掉如下的行前面的 “#”，最后一个"HandleLidSwitch" 的值改为Lock
[Login]
#NAutoVTs=6
#ReserveVT=6
#KillUserProcesses=no
#KillOnlyUsers=
#KillExcludeUsers=root
#InhibitDelayMaxSec=5
HandlePowerKey=poweroff
HandleSuspendKey=suspend
HandleHibernateKey=hibernate
HandleLidSwitch=lock
#HandleLidSwitchDocked=ignore
#PowerKeyIgnoreInhibited=no
#SuspendKeyIgnoreInhibited=no
#HibernateKeyIgnoreInhibited=no
#LidSwitchIgnoreInhibited=yes
#HoldoffTimeoutSec=30s
#IdleAction=ignore
#IdleActionSec=30min
#RuntimeDirectorySize=10%
#RemoveIPC=yes
#InhibitorsMax=8192
#SessionsMax=8192
#UserTasksMax=33%

#重启服务
systemctl restart systemd-logind
```

#### 包管理系统 (package management system, PMS)

#### 基于 Debian 的系统 (以 apt 为例)

* [apt官方wiki](https://wiki.debian.org/Apt)