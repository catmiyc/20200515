[toc]

# Qt 类库概述

> 对标准C++进行了扩充，引入了元对象系统、信号与槽、属性等特性
>
> Qt类库中大量的类是以模块形式分类组织的，包括基本模块和扩展模块等。

## 3.1 Qt核心特点

### 3.1.1 概述

> Qt本身不是一种编程语言，实际上是跨平台的C++开发类库。
>
> Qt元对象编译器（Meta-Object Compiler, MOC）是一个预处理器，在源程序编译前将这些Qt特性的程序转为C++兼容的形式，再由标准C++编译器进行编译。
>
> 这就是为什么信号与槽机制的类中，必须添加Q_OBJECT宏的原因，只有添加了这个宏，moc才能对类里面的信号与槽的代码进行预处理
>
> Qt Core 模块是Qt类库的核心，所有其他模块都依赖这个模块。

### 3.1.2 元对象系统

### 3.1.3 属性系统

1. 属性定义
2. 属性的使用
3. 动态属性

### 3.1.4 信号与槽

> 对象间进行通信的机制

#### 1. connect()函数的两种形式

#### 2. 使用sender()获得信号发射者

#### 3.自定义信号及其使用

### 3.1.5 元对象特性测试实例

## 3.2 Qt全局定义

<QtGlobal>

### 3.2.1 数据类型定义

### 3.2.2 函数

### 3.2.3 宏定义

## 3.3 容器类

### 3.3.1 容器类概述

> Qt提供了多个基于模板的容器类，这些容器类用于存储指定类型的数据项。
>
> 例如 ：QStringList 继承自  QList<QString>
>
> - 隐式共享和可重入的，进行了速度和存储的优化，减少可执行文件的大小
>
> - 线程安全的，作为只读容器时候可以被多个线程访问

QList<T>定义一个字符串列表的容器：

```c++
QList<QString> aList;
aList.append("Monday");
aList.append("Tuesday");
QString str = aList[0];
```

Qt的容器类分为顺序容器(sequential containers)和关联容器(associative containers)

### 3.3.2 顺序容器类

Qt顺序容器类： QList、QLinkedList、QVector、QStack和QQueue

#### 1 . QList

> 以数组列表形式实现的
>
> 常用函数： 插入 insert()、替换 replace()、 移动 move()、 删除 remove() 等

```cpp
//提供下表索引方式访问数据,提供at()函数
QList<QString> list;
list << "one" << "two" << "three" ;
QString str1 = list[1]; //str1 == "two"
QString str0 = list.at(0); //str0 == "one"
```

#### 2. QLinkedList

#### 3. QVector

> QVector<T> 提供动态数组的功能，以下表索引访问数据

### 3.3.3 关联容器类

Qt关联容器类：QMap、QMultiMap、QMultiHash、QSet

#### 1. QSet

> 基于离散列表的集合模板类，存储顺序不是一定的，查找值速度很快

```cPP
QSet <QString> set;
set << "dog" << "cat" << "tiger";
//测试一个值是否包含在这个集合,使用contains()
if(!set.contains("cat"))
    ...
```

#### 2. QMap

> QMap<Key, T> 提供一个字典（关联数组），一个键映射到一个值。

```
QMap <QString, int> map;
map["one"] = 1;
map["two"] = 2;
map["three"] = 3;
//也可以用insert()函数赋值，或remove()移除一个键值对
map.insert("four", 4);
map.remove("two");
//查找一个值，使用"[]", 或value()函数
int num1 = map["one"];
int num2 = map.value("two");
```

## 3.4 容器类的迭代

> 迭代器(iterator) 为访问容器类里的数据提供了统一的方法
>
> 两种迭代器： 
>
> Java 类型迭代器 和 STL类型迭代器
>
> Java类型的易于使用，且提供一些高级功能
>
> STL类型的效率更高
>
> Qt提供了关键字foreach用于方便访问容器里所有的数据项

### 3.4.1 Java类型迭代器

#### 1. Java类型迭代器其总表

> 对于每个容器类，有两个Java类型迭代器：一个用于只读操作，一个用于读写操作

| 容器类              | 只读迭代器       | 读写迭代器              |
| ------------------- | ---------------- | ----------------------- |
| QList<T>, QQueue<T> | QListIterator<T> | QMutableListIterator<T> |

#### 2. 顺序容器的迭代器的使用

```cpp
//遍历访问一个QList<QString>容器的所有数据项
QList<QString> list;
list << "a" << "b" << "c";
QListIterator<QString> i(list);
while(i.hasNext())
	qDebug() << i.next();
```

### 3.4.2 STL类型迭代器

#### 1. STL类型迭代器总表

| 容器类              | 只读迭代器               | 读写迭代器         |
| ------------------- | ------------------------ | ------------------ |
| QList<T>, QQueue<T> | QList<T>::const_iterator | QList<T>::iterator |

> STL类型的迭代器是数组的指针

#### 2. 顺序容器类的迭代器的用法

```c++
//将QList<QString> list里的数据项逐项输出
QList<QString> list;
list << "a" << "b" << "c";
QList<QString>::cosnt_iterator;
for(i = list.constBegin() i != list.constEnd(); ++i)
	qDebug() << *i;
```

### 3.4.3 foreach 关键字

```c++
foreach (variable, container)
```

```
//使用foreach 遍历一个QLinkedList<QString>
QLinkedList <QString> list;
...
QString str;
foreach(str, list)
	qDebug() << str;
```

## 3.5 Qt类库的模块

> Qt类库里大量的类根据功能分为各种模块。
>
> - Qt基本模块(Qt Essentials)：基本功能
> - Qt附加模块(Qt Add-Ons)：
> - 增值模块等

