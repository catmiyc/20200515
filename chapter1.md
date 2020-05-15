[toc]

## 1. 下载和安装

下载离线安装包

![下载和安装](C:\Users\catmi\AppData\Roaming\Typora\typora-user-images\image-20200515110945980.png)	

Qtcreator 是用于开发Qt程序的IDE, 是Qt的主要工具软件

关于MSVC2015编辑器图标黄色感叹号

​	Debugger页面没有Windows的CDB调试器，可以编译但不能调试

​	缺少Windows Software Development Kit(SDK)

​	这个SDK不会跟VS一块安装，需要从Microsoft网站下载

​	下载： Windows Software Development Kit for Windows 8.1

## 2. Hello World

3种窗口的基类：

1. QMainWindow 主窗口类，主窗口具有主菜单栏，工具栏和状态栏，类似于一般应用程序的主窗口
2. QWidget 是**所有具有可视界面类**的基类，选择QWidget创建的界面对各种界面组件都支持
3. QDialog是对话框类，可建立一个基于对话框的界面

