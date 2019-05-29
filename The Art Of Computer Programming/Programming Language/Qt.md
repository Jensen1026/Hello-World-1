# Qt

[TOC]

## Windows下环境搭建

* 开发环境：Windows10 pro + Visual Studio 2019 + Qt5.12.3
* [Qt官网](<https://www.qt.io/cn>)
* [Qt官方文档](<http://doc.qt.io/>)
* [Qt下载链接](<http://download.qt.io/archive/qt/> )
* 假设已安装配置好Visual Studio 2019

### 安装过程

* 安装Qt

  在上述下载链接中选择合适版本的 Qt 下载并打开，选择合适的组件进行安装，比如我就只选择了下面这两个组件：

  ![](.\Pictures\Qt1.png)


* 安装 Visual Studio 插件

  在 Vs 中搜索 Qt Visual Studio Tools 并安装，并在 Qt 插件中配置好环境变量，比如我是这样配置的：
  
  ![](.\Pictures\Qt2.png)

### 测试

在 Vs 中新建一个 Qt GUI Application 项目，将项目文件内容改为：

```c++

#include <QApplication>
#include <QLabel>
 
int main(int argc, char *argv[])
{
    QApplication app(argc, argv);
    QLabel *label = new QLabel(" <h2> <i> I Love You </i> " "<font color = red >Qt</font> </h2>");
    label->show();
    return app.exec();
}
```

运行结果为：

![](.\Pictures\Qt3.png)

## Linux 下环境搭建

## Qt学习

### 示例

