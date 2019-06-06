# Linux notes
[TOC]

## Linux Desktop

### OS

* Gentoo
* Deepin

## Linux Server

### OS

* Ubuntu Server (Debian)
* Centos (Red Hat)
* Gentoo

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

###### [Kde]()

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

#### 基于 Red Hat 的系统  (以 yum 为例)

* 列出系统上已安装的包

  ```bash
  yum list installed
  ```

* 查看某个特定的包是否安装

  ```bash
  yum list package_name
  ```

* 找出系统上的某个特定文件属于哪个软件包

  ```bash
  yum provides file_name
  #此时 yum 会分别查找三个仓库：base、updates 和 installed
  ```

* 使用 yum 安装 rmp 包

  ```bash
  yum localinstall package_name.rpm
  ```

* 使用 yum 更新软件

  * 列出所有已安装包的可用更新

    ```bash
    yum list updates
    ```

  * 更新某个特定软件包

    ```bash
    yum update package_name
    ```

  * 更新所有软件包

    ```bash
    yum update
    ```

* 卸载软件

  * 只删除软件包而保留配置文件和数据文件

    ```bash
    yum remove package_name
    ```

  * 删除软件包和他所有的文件

    ```bash
    yum erase package_name
    ```

* 处理损坏的包依赖关系 (broken dependency)

  ```bash
  #依次尝试以下每个命令看是否有效
  yum clean all;yum update
  yum deplist package_name
  yum update --skip-broken
  ```

* 列出 yum 软件仓库

  ```bash
  yum repolist
  #yum 的仓库定义文件位于 /etc/yum.repos.d
  ```

  

  

  