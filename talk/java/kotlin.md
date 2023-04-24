
# 第一行代码 Android 第3版

**Author：郭霖**

--------


+ [目录](#目录)
+ [第一行代码 Android 第3版](#第一行代码-android-第3版)
  * [Android](#android)
    - [Linux内核层](#linux内核层)
    - [系统运行库层](#系统运行库层)
    - [应用框架层](#应用框架层)
    - [应用层](#应用层)
  * [requirement](#requirement)
  * [四大组件](#四大组件)
  * [Android-Studioo](#android-studioo)
    - [目录格式](#目录格式)
  * [Kotlin](#kotlin)
    - [语言学习](#语言学习)





## Android

它的系统架构大致可分为4个部分：
- Linux内核层
- 系统运行库层
- 应用框架层
- 应用层

### Linux内核层

基于Linux内核，为Android设备的各种硬件提供了底层的驱动如：
- 显示驱动
- 音频驱动
- 相机驱动
- 蓝牙驱动
- Wi-Fi驱动
- 电源管理

### 系统运行库层

通过一些C/C++库为其提供主要的特性支持：
- SQLite库 数据库
- OpenGL/ES库 3D和绘图的支持
- Webkit库 浏览器内核
- Android运行时库 Dalvik虚拟机，后改为ART

### 应用框架层

提供构建应用程序时可能用到的各种API

### 应用层

开发运行在上面的程序

## requirement

- JDK
- Android SDK
- Android Studio, Google推出的IDE

> https://developer.android.google.cn/studio
> http://www.android-studio.org 国内代理点
> sudo pacman -S android studio

## 四大组件

- Activity
- Service
- BroadcastReceiver
- ContentProvider

--------

## Android-Studioo

### 目录格式

1. .gradle和.idea
> 放置Android Studio自动生成的一些文件，无须关心，不用编辑
2. app
> 项目中的代码、资源等内容
4. >




--------

# Kotlin

目前谷歌推出用于开发安卓的主要编程语言，类似JAVA，但有其谷歌的编程风格

## 语言学习

### 变量

 在Kotlin中定义变量的方式和Java区别很大，但同go相似，毕竟是同家公司。

在Java中定义一个变量需要在前面声明其的类型，Kotlin只有两个关键字在前面：
- val(value) 用于声明一个不可变的变量，初始赋值后则不可更改，类似Java的final或Go的const
- var(variable) 用于声明一个可变的变量，初始赋值后仍可更改

与Java不同的是，Kotlin有出色的类型推导机制同Go类似，但在对一个变量延迟赋值的情况下不是很出色，需要显示声明

> var a: Int = 10 #Int的首字母大写

其表示完全抛弃了Java的基本数据类型，全部使用了对象数据类型。它拥有自己的方法和继承结构。

Kotlin这样设计是为了解决Java中final关键字没有被合理使用的问题

- 在Java中，除非主动声明final，否则就是可变的。

- 一个好的编程习惯，除非一个变量明确允许被修改，否则都应当加上final关键字。
- 作者技巧：永远优先使用val声明一个变量，当其没有满足需求时再使用var。

注意，Kotlin的每一行末尾不需要分号

| Java基本数据类型 | Kotlin对象数据类型 | 数据类型说明 |
|------------------|--------------------|--------------|
| int              | Int                | 整型         |
| long             | Long               | 长整型       |
| short            | Short              | 短整型       |
| float            | Float              | 单精度浮点型 |
| double           | Double             | 双精度浮点型 |
| boolean          | Boolean            | 布尔型       |
| char             | Char               | 字符型       |
| byte             | Byte               | 字节型       |

### 函数

区别函数与方法
> 同一个概念，英文翻译的区别而已
> Java多叫方法，Kotlin多叫函数

main()是程序的入口

```kotlin
fun methodName(param1: Int, Param2: Int): Int{
return 0
} //同Go类似
```
声明格式：

> 参数名:参数类型，可写返回类型<br>
> 函数体，在大括号中

当在使用内置函数时最好使用Android Studio的自动补全，应为需要导入函数包。

语法糖
当一个函数中只有一行代码时，Kotlin允许我们不必编写函数体，可以直接将唯一的一行代码写在函数定义的尾部，中间用等号连接即可。

```kotlin
fun largerNumber(num1:Int, num2: Int): Int = max(num1, num2)
// 省略了return 也可运用类型推导省略返回值的声明
fun largerNumber(num1:Int, num2: Int) = max(num1, num2)

```

### 程序的逻辑控制
















