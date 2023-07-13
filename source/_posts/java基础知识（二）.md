---
title: java学习之路--基础知识（二）
author: yuansir


summary: java学习之路的笔记总结
categories: Java 笔记
tags:
  - blog
  - hexo
abbrlink: 15
date: 2023-07-10 21：30：15
---
# java中字符串基础知识（二）
1. String 注意点
 字符串的内容是不会发生改变的，它的对象在创建后不能被更改。
2. 创建字符串对象
- 直接复制
- new
```java
//空参构造：获取一个空白的字符串对象
 String s1=new String()
 //传递一个字符串，根据字符串传递的内容再创建一个新的字符串对象
 String s2=new String("abc");
 //传递一个字符数组，根据字符数组的内容再创建一个新的字符串对象
 //需求：修改字符串的内容 abc->Qbc
//abc==>{'a','b','c'}
char[] chs={'a','b','c','d'};
String s3=new String(chs);

//传递一个字节数组，根据字节的数组的内容在创建一个新的字符串对象
//应用场景：在网络中传输的数据其实都是字节信息
//我们一般要把字节信息进行转换，转成字符串，此实际需要用到这个构造了
byte[] bytes={97,98,99,100};
String s4=new String(bytes);

```
3. 字符串比较
- 基本数据类型比较：比较的是数据值
- 引用数据类型比较：比的是地址值
- equals 比较字符串内容是否相等
```java
String s1="123";
String s2="abc";
boolean result1=s1.equals(s2)
```
- equalsIgnoreCase 比较字符串的内容是否相等，忽略大小写
```java
boolean result2=s1.equalsIgnoreCase(s2);
```
4. 遍历字符串
- public char charAt(int index)： 根据索引返回字符
- public int  length():返回字符串的长度
- 注意：数组名.length    字符串对象.length()
5. 统计字符个数
```java
    public static void main(String[] args) {
        //键盘输入一个字符串
        System.out.println("请输入一个包含大小写字母及数字的字符串");
        Scanner r=new Scanner(System.in);
        String str=r.next();
        int bigCount=0;//大写字母数
        int smallCount=0;//小写字母数
        int numCount=0;//数字字符数
        for(int i=0;i< str.length();i++){
            int temp=str.charAt(i);
            if(temp>=65&&temp<=90){
                bigCount++;
            }else if(temp>=97 && temp<=122){
                smallCount++;
            }else{
                numCount++;
            }
        }
        System.out.println("大写字母数："+bigCount);
        System.out.println("小写字母数："+smallCount);
        System.out.println("数字字母数："+numCount);
    }
```
6. 字符串拼接和反转
```java
    public static String reverser (String str) {
        String result="";
        for (int i = str.length()-1; i >=0 ; i--) {
            char c=str.charAt(i);
            result+=c;
        }
        return result;
    }
```
7. 字符串截取
- String substring(int beginIndex,int endIndex) 注意：左闭右开
```java
     String phone="13245698712";
        //截取手机号前三位
        String start= phone.substring(0,3);
        //截取手机号后四位
        String end=phone.substring(7);
        //拼接
        String result=start +"****"+end;
        System.out.println(result);
```
8. StringBuilder
他可以看成一个可变的容器，里面的内容是可以变化的，不像字符串一样不可变，可以提高字符串的操作效率，可以将容器里面的内容反转。
- public StringBuilder append() //添加元素
- publick StringBuilder reverse()  //反转容器中的内容
- public int length() //返回长度
- public String toString()  //将StringBuilder 转换成字符串。
```java
//传统字符串操作
String s1=s2+s3+s4+s5;//在这个字符串拼接的过程中会产生很多新的字符串。
       //创建对象
        StringBuilder sb=new StringBuilder();
        //添加字符串
        sb.append("aaa").append("bbbb").append("2sad");
        //将StringBuilder 转换成String
        sb.toString();
```
9. 判断是否是对称字符串
```java
     //键盘输入一个字符串
        Scanner r=new Scanner(System.in);
        System.out.println("请输入一个字符串");
        String str=r.next();
        //创建对象
        String result=new StringBuilder().append(str).reverse().toString();
        if(str.equals(result)){
            System.out.println("当前字符串是对称字符串");
        }else{
            System.out.println("当前字符串不是对称字符串");
        }
```
10. StringJoiner
它也可以看成一个容器，容器内容是可以变化的；可以提高字符串的操作效率，而且代码编写特备简介，JDK8之后才出现的
- 格式
    StringJoiner sb=new StringJoiner("间隔符号"，"开始符号"，"结束符号")
- add(添加的内容) //添加数据，并返回对象本身
- length() //返回长度
- toString()  //转换成字符串
11. 字符串原理
- 字符串存储内存原理
  直接赋值的会复用字符串常量池中的；new出来的不会复用，会开辟一个新的内存空间。
- == 比较的是什么？
 基本类型比较的是值，引用数据类型比较的是地址。
- 字符串拼接原理
 如果没有变量参与，都是字符串直接相加，编译之后就是拼接之后的结果，会复用串池中的字符串
 如果有变量参与，会创建新的字符串，浪费内存。
 - StringBuilder 提高效率原理图
  所有要拼接的内容都会往StringBulder中放，不会创建很多无用的空间，节约内存。
