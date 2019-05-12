* Docker

** docker 原理

*** 容器规范

    OCI (Open Container Initiative) 组织

    runtime spec 和 image format spec 规范

*** 容器 runtime 
    runtime 是容器真正运行的地方。runtime 需要跟操作系统 kernel 紧密协作，为容器
    提供运行环境。

**** 三种主流容器 runtime

     * lxc

     * runc: Docker 默认 runtime

     * rkt

*** 容器管理工具 

    runc 的管理工具是 docker engine，包含 deamon 和 cli 两部分。 

*** 容器定义工具

**** docker image

     docker image 是 docker 容器的模板，runtime 依据 docker image 创建容器。

**** dockerfile

     dockerfile 是包含若干命令的文本文件，可以用来创建 docker image

**** ACI (App Container Image)

     CoreOS 开发的 rkt 容器的 image 格式。

*** Registry

    Registry 是存放 docker image 的仓库。

*** 容器编排引擎

    Kubernetes [kubə'netis]

*** 容器网络

    * docker network

    * flannel

    * weave

    * calico

*** Docker 架构

**** Docker 采用的是 Client/Server 架构，核心组件包括：

     * Docker 客户端 - Client

     * Docker 服务器 - Docker daemon

     * Docker 镜像 - Image

     * Registry

     * Docker 容器 - Container

       [[./images/ ]

       Docker 架构图

*** 理解容器镜像
**** base 镜像

     base 镜像有两层含义：

     1. 不依赖其他镜像，从 scratch 构建。

     2. 其他镜像可以之为基础进行扩展。

**** rootfs
     
     挂载在容器根目录上，用来为容器进程提供隔离后执行环境的文件系统，就是所谓的
     rootfs 或者 “容器镜像”。

     一致性：由于 rootfs 里打包的不只是应用，而是整个操作系统的文件和目录，也就
     意味着，应用以及它运行所需要的所有依赖，都被封装在了一起。对一个应用来说，
     操作系统本身才是它运行所需要的最完整的 “依赖库“。这种深入到操作系统级别的
     运行环境一致性，打通了应用在本地开发和远端执行环境之间难以逾越的鸿沟。

**** 层 (layer)

     Docker 在镜像的设计中，引入了层 (layer) 的概念。也就是说，用户制作镜像的每
     一部操作，都会生成一个层，也就是一个增量 rootfs。

***** 联合文件系统 (Union File System)

      Union File System 也叫 UnionFS，最主要的功能是将多个不同位置的目录联合挂载
      (union mount) 到同一个目录下。

      AuFS (Advance UnionFS)

**** 镜像的分层结构

***** 只读层

***** 可读写层

***** Init 层

***** Copy-on-Write 特性
     
*** Cgroups

    Linux Cgroups 的全称是 Linux Control Group。它最主要的作用，就是限制一个进程
    组能够使用的资源上限，包括 CPU、内存、磁盘、网络带宽等等。

    在 linux 中，Cgroups 给用户暴露出来的操作接口是文件系统，即它以文件和目录的
    方式组织在操作系统的 /sys/fs/cgroup 路径下。

    Docker 如何操作 Cgroups:

    Cgroups 对资源限制不完善的地方：

    /proc 文件系统问题：/proc 文件系统不了解 Cgroups 限制的存在。如：在容器内执
    行 top 命令显示的不是容器的 CPU 和内存数据，而是宿主机的。
    
*** Namespace
    
    Namespace 技术则是用来修改进程视图的主要方法。

    Mount Namespace，用于让被隔离进程只看到当前 Namespace 里的挂载点信息。它对容
    器进行视图的改变，一定是伴随着挂载操作 (mount) 才能生效。Mount Namespace 是
    基于对 chroot (change root file system) 的不断改良才被发明出来的。

    Network Namespace，用于让被隔离进程看到当前 Namespace 里的网络设备和配置。

*** 虚拟机和容器对比

    [[./虚拟机和容器的对比图]]

    虚拟机的工作原理。其中，名为 Hypervisor 的软件是虚拟机最主要的部分。它通过硬
    件虚拟化功能，模拟出了运行一个操作系统所需要的各种硬件，比如 CPU、内存、I/O
    设备等。然后，它在这些虚拟的硬件上安装了一个新的操作系统，即 Guest OS。

    优点：

    缺点：额外的资源消耗和占用

    Docker：容器是一个“单进程”模型。

    优点：敏捷”和“高性能”，“一致性”。

    缺点：隔离得不彻底。可以使用 Seccomp 等技术，对容器内部发起的所有系统调用进
    行过滤和甄别来进行安全加固，但这种方法因为多了一层对系统调用的过滤，一定会拖
    累容器的性能。

*** 对于 Docker 项目来说，它最核心的原理实际上就是为待创建的用户进程：

    1. 启用 Linux Namespace 配置；

    2. 设置指定的 Cgroups 参数；

    3. 切换进程的根目录 (Change Root)。

    这样，一个完整的容器就诞生了。不过，Docker 项目在最后一步的切换上会优先使用
    pivot_root 系统调用，如果系统不支持，才会使用 chroot。
    
*** Volume

**** 绑定挂载 (bind mount)

     允许你将一个目录或者文件，而不是整个设备，挂载到一个指定的目录上。并且，这
     时你在该挂载点上进行的任何操作，只是发生在被挂载的目录或者文件上，而原挂载
     点的内容则会被隐藏起来且不受影响。

** 基本操作

*** docker 命令

**** docker pull

     从 Registry 下载镜像。

**** docker run
      
     先下载镜像（如果本地没有），然后再启动容器。

**** docker images

     列出镜像信息。

**** docker ps

     列出容器信息。
