Learning how to use Development tools on windows

[TOC]

## Visual Studio

### 基本概念
* Visual Studio 使用项目来组织应用的代码，使用解决方案来组织项目。 项目包含用于生成应用的所有选项、配置和规则。 它还负责管理所有项目文件和任何外部文件间的关系。 要创建应用，需首先创建一个新项目和解决方案。
* Visual Studio默认使用微软的 - Microsoft Visual C++ Compiler（cl.exe）来编译程序，使用 
  Debugging Tools for Widows（cdb.exe）来调试程序。

### 快捷键

* File

  ![](.\Pictures\vs-file.png)

* Edit

  ![](.\Pictures\vs-edit.png)

* View

  ![](.\Pictures\vs-view.png)

* Project

  ![](.\Pictures\vs-project.png)

* Build

  ![](.\Pictures\vs-build.png)

* Debug

  ![](.\Pictures\vs-debug.png)


* Ctrl + Shift + S	Save all
* Ctrl + \ + T	Task List
* Ctrl + Q	Search Visual Studio

#### 项目相关的快捷键

* Ctrl + Shift + B	生成项目
	Ctrl + Alt + L	显示Solution Explorer（解决方案资源管理器）
	Shift + Alt+ C	添加新类
	Shift + Alt + A	添加新项目到项目  

#### 编辑相关的键盘快捷键

* Ctrl + Enter	在当前行插入空行
* Ctrl + Shift + Enter	在当前行下方插入空行
* Ctrl +空格键	使用 IntelliSense（智能感知）自动完成
* Alt + Shift +箭头键(←,↑,↓,→)	选择代码的自定义部分
* Ctrl + }	匹配大括号、括号
* Ctrl + Shift +}	在匹配的括号、括号内选择文本
* Ctrl + Shift + S	保存所有文件和项目
* Ctrl + K，Ctrl + C	注释选定行
* Ctrl + K，Ctrl + U	取消选定行的注释
* Ctrl + K，Ctrl + D	正确对齐所有代码
* Shift + End	从头到尾选择整行
* Shift + Home	从尾到头选择整行
* Ctrl + Delete	删除光标右侧的所有字

#### 导航相关的键盘快捷键

* Ctrl +Up/Down	滚动窗口但不移动光标
* Ctrl + -	让光标移动到它先前的位置
* Ctrl ++	让光标移动到下一个位置
* F12	转到定义  

#### 调试相关的键盘快捷键

* Ctrl + Alt + P	附加到进程
* F10	调试单步执行
* F5	开始调试
* Shift + F5	停止调试
* Ctrl + Shift + F5	Restart
* Ctrl + Alt + Q	添加快捷匹配
* F9	设置或删除断点  
* 
#### 搜索相关的键盘快捷键

* Ctrl + K  Ctrl + K	将当前行添加书签

* Ctrl + K  Ctrl + N	导航至下一个书签

* Ctrl + .	如果你键入一个类名如Collection<string>，且命名空间导入不正确的话，那么这个快捷方式组合将自动插入导入

* Ctrl + Shift + F	在文件中查找

* Shift  + F12	查找所有引用

* Ctrl + F	显示查找对话框

* Ctrl + H	显示替换对话框

* Ctrl + G	跳转到行号或行

* Ctrl + Shift + F	查找所选条目在整个解决方案中的引用  

* Ctrl + T

  

[Visual Studio 中的默认键盘快捷方式](<https://docs.microsoft.com/zh-cn/visualstudio/ide/default-keyboard-shortcuts-in-visual-studio?view=vs-2019>)

### Extensions

*

### Q&A

* Vi­sual Stu­dio 更新之后原先的项目不能编译，提示无法打开源文件 xxx.h

  ```text
  1.在【解决方案资源管理器】中右键项目，选择 【properties】
  2.在打开窗口中选择 【General】，将右侧【Windows SDK Version】下拉选择新的 SDK 版本即可。
  ```



## Visual Studio Code

### 快捷键

* Ctrl + K Ctrl + S	Keyboard Shortcuts
* Ctrl + P	Quick Open, Go to File...
* Ctrl + ,	User Settings
* Ctrl + Shift + P	Show Command palette
* Ctrl + .	Quick fix
* Ctrl + /	Toggle Line Comment
* F8	Go to next problem in files
* Alt + F8	Go to next problem
### 扩展

*

## WSL

* Kaili Linux
* Windows Terminal

### 基本操作

* 使用 Windows 文件资源管理器访问 WSL 文件系统：

  ```bash
  #运行以下命令
  explorer.exe .
  #注意不要漏掉后面的“空格+点”
  ```

  