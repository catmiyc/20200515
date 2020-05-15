[toc]

# 2.1 UI文件设计与运行机制

## 2.1.1 项目文件组成

## 2.1.2 项目管理文件

加入core gui 模块；用于GUI设计的类库模块

如果是控制台(console)应用程序，就不需要添加core gui

如果用到了设计数据库操作的，就需要添加sql模块

Qt	+= sql

## 2.1.3 界面文件

- 对象浏览器Object Inspector
  - 对象名称(ObjectName)和类名称
- 属性编辑器Property Editor

QObject--QWidget--QFrame--QLabel

## 2.1.4 主函数文件

```c++
//main.cpp是实现main()函数的文件
#include "widget.h"
#include <QApplication>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);//定义并创建应用程序
    Widget w;                  //定义并创建窗口
    w.show();                  //显示窗口
    return a.exec();           //应用程序运行
}

```

>- main()函数是程序的入口。只要功能就是创建宽口，显示窗口，并运行用程序，开始应用程序的消息循环和事件处理
>
>- QApplication是Qt的标准应用程序类，创建一个QApplication类的实例a，这个就是应用程序对象
>
>- 定义一个Widget类的变量w，Widget是本实例设计的窗口的类名。
>
>- 再用w.show()显示该窗口。

## 2.1.5 窗体相关的文件

