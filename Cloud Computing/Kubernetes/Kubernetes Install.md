# Kubernetes 安装

[TOC]

## 部署 Kubernetes

### 环境

* OS: Centos  7.6.1810
* RAM: 4G
* 全程使用 root 这一用户 

### 代理

#### 安装 shadowsocks

```bash
yum install -y python-pip
pip install shadowsocks
```

安装完之后会有两个命令：sslocal 和 ssserver。前者为客户端、后者为服务器端，在此我们只使用 sslocal 这一命令。

#### 建立配置文件：shadowsocks.json

```json
{
  "server":"your ss server ip address",
  "local_address": "127.0.0.1",
  "local_port":1080,
  "server_port":your ss server port,
  "password":"your password",
  "timeout":300,
  "method":"aes-256-cfb"
}
```

我的是在：/root/shadowsocks.json

#### 启动 ss 客户端

使用以下命令启动 sslocal:

```bash
#机器每次重启都需要执行一遍，可以将其加入例行性任务中
sslocal -c shadowsocks.json -d start  
```

#### 安装代理工具

在这里我们选择简单易用的 privoxy，详细使用方法请参考 [ArchWiki]()

```bash
yum install epel-release  
yum install -y privoxy  
#删除多安装的无用repo  
rm /etc/yum.repos.d/epel-testing.repo   
```

#### 编辑配置文件: /etc/privoxy/config

```bash
vim /etc/privoxy/config 
#搜索 socks5t在下面添加一条转发代理ip 
forward-socks5t   /               127.0.0.1:1080 .
#然后搜索listen-address，取消注释的ip地址，或直接新添加下面的信息
listen-address  127.0.0.1:8118  
```

#### 配置终端

```bash
#编辑 .bashrc 或 .zshrc 添加下面信息
export http_proxy=http://127.0.0.1:8118  
export https_proxy=http://127.0.0.1:8118  
export ftp_proxy=http://127.0.0.1:8118  
```

之后使用 source ~/.bashrc 或 source ~/.zshrc 重新加载配置文件

#### 重启 privoxy

```bash
#每次修改 /etc/privoxy/config 之后都需要执行一次
systemctl restart privoxy.serivce  
```

#### 测试

```bash
#看到有响应信息就代表成功了，但此时可能任然 ping 不通
curl www.google.com
```

### Docker 
#### 安装 Docker

```bash
yum -y install docker
```

#### 设置开机启动

```bash
service docker start
systemctl enable docker
```

#### 验证 Docker 是否安装成功

```bash
docker run hello-world
```

#### 配置 Docker 代理

```bash
#编辑配置文件
vim /usr/lib/systemd/system/docker.service
#添加以下内容
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:8118"
#保存后重启 Docker
systemctl daemon-reload
systemctl restart docker
```

### Kubernetes

#### 安装 Kubeadm, Kubelet 和 Kubectl

```bash
#Centos, RHEL or Fedora
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
exclude=kube*
EOF

# 将 SELinux 设置为 permissive 模式(将其禁用)
setenforce 0
sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

systemctl enable kubelet && systemctl start kubelet
```

一些 RHEL/CentOS 7 的用户曾经遇到过：由于 iptables 被绕过导致网络请求被错误的路由。您得保证 在您的 `sysctl` 配置中 `net.bridge.bridge-nf-call-iptables` 被设为1：

```bash
cat <<EOF >  /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sysctl --system
```

#### 在 Master 节点上配置 kubelet 所需的 cgroup 驱动

使 kubelet 的 Cgroup Driver 与 Docker 的 Cgroup Driver 一致，Kubelet 使用的默认值为: cgroupfs。

```bash
#编辑配置文件
vim /usr/lib/systemd/system/kubelet.service.d/10-kubeadm.conf
#添加以下内容，使用 docker info 命令查看 Docker 的 Cgroup Driver
Environment="KUBELET_CGROUP_ARGS=--cgroup-driver=systemd"
```

#### 重启 Kubelet

```bash
systemctl daemon-reload
systemctl restart kubelet
```

#### 关闭 swap

```bash
#临时关闭 swap
swapoff -a
#要永久禁掉swap分区，打开如下文件注释掉swap那一行
vim /etc/fstab
```

#### 取消代理

若不取消代理在使用 kubeadm init 的是时候会报错: 

```text
Unable to update cni config: No networks found in /etc/cni/net.d

Container runtime network not ready: NetworkReady=false reason:NetworkPlugin
```

#### 初始化 Master

```bash
kubeadm init
```

#### 安装网络组件Flannel

```bash
yum install -y flannel
```

#### 安装 Dashboard （Master 节点）

```bash
#运行 Dashboard	
kubectl proxy
#默认绑定8001端口，且只允许本机访问，如果想要全世界都能访问就得加个启动参数--accept-hosts='^*$' &
nohup kubectl proxy --address='10.148.177.252' --port=8989 --accept-hosts='^*$' &
```

#### 基本操作



#### Troubleshooting

*  kubelet 日志中有如下错误：`Unable to update cni config: No networks found in /etc/cni/net.d`

  ```text
  解决办法：
  这种情况考虑是开了系统代理导致，由于可能是全局代理，导致 IP 访问API Server 也是不通的，通常建议此时关闭系统代理，仅仅开启 Docker 代理就足够应付接下来的安装。
  ```

  



