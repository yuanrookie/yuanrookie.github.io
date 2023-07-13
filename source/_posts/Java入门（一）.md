---
title: java环境工具安装和基本知识了解
author: yuansir


summary: 小白第一次接触java,通过跟随视频学习，总结学习java的一些基础知识，方便后面回顾复习
categories: Java
tags:
  - blog
  - hexo
abbrlink: 13
date: 2023-07-09 20：40：25
---

# java环境工具安装和基本知识了解

## 一、cmd常见米命令
1. 《 D: 》 切换到对应盘符中
2. 《 dir》 查看当前路径下的内容
3. 《cd  和 cd..》 进入单级目录或者返回上一级目录
4. 《cd 目录1\目录2 和 cd \》 进入多级目录或者回退到盘符
5. 《cls 和exit》 清屏 和退出命令提示符窗
## 二、java环境工具安装流程
1. jdk安装
> [jdk安装教程](https://blog.csdn.net/weixin_44778232/article/details/124610021)
2. idea下载安装教程
> [idea下载安装教程](https://blog.csdn.net/ACE_U_005A/article/details/114882838)
> [idea配置教程](https://blog.csdn.net/ACE_U_005A/article/details/125552411)
3. maven安装教程
> [maven安装教程](https://blog.csdn.net/u012660464/article/details/114113349)
4. IDEA实用插件
- 生成标准javabean类  安装PTG插件
## 三、java中基础知识了解
> [java入门教程上](https://www.bilibili.com/video/BV17F411T7Ao/?spm_id_from=333.337.search-card.all.click&vd_source=ee23caf8ba13ec874dfa7f165dce3c31)
1. jdk,jre,jvm三者之间的关系
 - JDK是java开发工具包，包括 JVM虚拟机（java 运行的地方），核心类库(Java已经写好的工具)，开发工具（如 javac,java,jdb,jhat）
 - JRE是Java运行环境,由JVM,核心类库，运行工具组成
 - JDK包含了JRE，JRE包含了JVM
2. 注释
- 单行注释 //内容    快捷键 ctrl +/
- 多行注释 /*内容*/  快捷键：ctrL+shift+/
- 文档注释  /**内容*/
3. 字面量分类
- 整数 如77
- 小数如22.2
- 字符串 如 "jkdsahjd"
- 字符类型 如 'a'
- 布尔类型 如 false
- 空类型 如 void
- 特殊字面量 \t 制表符（把前面字符串的长度补齐到8，或者8的整数倍；最少补一个空格，最多补八个空格）
```java
 SyStem.out.println("name"+'\t'+ "age")
 SyStem.out.println("tom"+'\t'+ "23")
 //实际效果
 name    age
 tom     23
```
4. 数据类型
数据类型分为基本数据类型和引用数据类型两类
- 基本数据类型
基本数据类型分为四大类八个变量；

 | 数据类型 | 关键字 |     取值范围     | 范例|
 | -------  | :-----: | -------  | ------|
 | 整数  | byte | -128~127  |  byte emp = 12
 | 整数  | short | -32768~32767  |  byte emp = 12
 | 整数  | int  | 10位数  |  byte emp = 12
 | 整数  | long | 19位数  |  byte emp = 12L
 | 浮点数  | float | -3.401298e-38到3.402823e+38  |  float emp = 12.1F
 | 浮点数  | double | -4.90000000e-324到1.797693e+308  |  double emp = 12.1
 | 字符  | char | 0-65535  |  char emp = 'a'
 | 布尔类型  | boolean | true,false  |  char emp =false
5. 标识符命名方法
标识符是由字母数字下划线和$组成；不能采用关键字；不能以数字开头；区分大小写；标识符名要见名知意
- 方法，变量采用小驼峰命名
- 类名 采用大驼峰命名
6. idea中快捷键方式
-  快速创建一个模板
```java
  //psvm+回车 可以快速创建以下模板
    public static void main(String[] args) {

    }
```
- 快速创建一个输出语句 sout+回车
```java
        System.out.println();
```
7. API帮助文档
链接: https://pan.baidu.com/s/1_Zlr731rtXiy5HGzwT56iA 提取码: ndpc 复制这段内容后打开百度网盘手机App，操作更方便哦
当下载完毕之后，右击这个文件，点击属性，把解除锁定勾选上，即可正常使用。
