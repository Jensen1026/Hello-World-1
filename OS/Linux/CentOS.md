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