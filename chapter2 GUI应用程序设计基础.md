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

>- main()函数是程序的入口。主要功能就是创建窗口，显示窗口，并运行用程序，开始应用程序的消息循环和事件处理
>
>- QApplication是Qt的标准应用程序类，创建一个QApplication类的实例a，这个就是应用程序对象
>
>- 定义一个Widget类的变量w，Widget是本实例设计的窗口的类名。
>
>- 再用w.show()显示该窗口。

## 2.1.5 窗体相关的文件

| 文件       | 功能                               |
| ---------- | ---------------------------------- |
| widget.h   | 定义窗体类的头文件，定义了类Widget |
| widget.cpp | Widget类的功能实现源程序文件       |
| widget.ui  | 窗体界面文件                       |

1. 类Widget继承自窗体基类QWidget

   1.1 namespace声明

```c++
namespqce Ui{ class Widget;}
```

声明了一个名为Ui的命名空间(namespace)，包含了一个类Widget，但这个类步是本文件里定义的类Widget，而是ui_widget.h文件中定义的类，用于描述界面组件的。	

​       1.2 

```c++
class Widget : public QWidget
{
	Q_OBJECT
public:
	Widget(QWidget *parent = nullptr);
	~Widget();
private:
	Ui::Widget *ui;
};
```

Widget类中使用了宏Q_OBJECT，这是使用Qt的信号和槽机制必须加入的一个宏

*ui 是前面声明的namespace Ui里的Widget类来定义的，所以ui是指向可视化设计界面的。

2. widget.cpp文件

```c++
Widget::Widget(QWidget *parent) : QWidget(parent), ui(new Ui::Widget)
{
    ui->setupUi(this);
}
```

执行父类QWidget的构造函数，创建一个Ui::Widget类的对象ui。

setupUi()函数，实现窗口的生成与各种属性的设置、信号与槽的关联

# 2.2 可视化UI设计

### 信号与槽：

QObject::connect(sender, SIGNAL(siginal(), reveiver, SLOT(slot()));

connect()是QObject类的一个静态函数，QObject是所有Qt类的基类，在实际调用中忽略

直接写为：

connect(sender, SIGNAL(siginal(), reveiver, SLOT(slot()));

SIGNAL 和 SLOT是Qt的宏，用于指明信号和槽，并将他们的参数转换为相应的字符串。

例如：

connect(btnClose, SIGNAL(clicked()), Widget, SLOT(close()));

1. 一个信号可以连接多个槽
   1. 槽函数按照建立连接时的顺序依次连接
2. 多个信号可以连接同一个槽函数
3. 一个信号连接另外一个信号
   1. 当一个信号发射也会发射另外一个信号，实现某些特殊的功能

**信号与槽机制是QtGUI编程的基础**

### 可视化 生成槽函数原型和框架

1. 字体样式设置

void on_<object name>__<signal name>(<signal parameters);

void on_chkBoxUnder_clicked(bool checked);

connect(chkBoxUnder, SIGNAL(clicked(bool)), this, SLOT(on_chkBoxUnder_clicked(bool));

2. 字体颜色设置

3. 三个按钮的功能设计

确定，取消，退出三个按钮

accept(), reject(), close()



# 2.3 代码化UI设计

