---
title: java学习之路--基础知识（一）
author: yuansir


summary: java学习之路的笔记总结
categories: Java 笔记
tags:
  - blog
  - hexo
abbrlink: 14
date: 2023-07-10 21：25：20
---
# java基础知识（一）
## 一、运算符
1. 算数运算符(加减乘除取余)

```java
       // +
        System.out.println(3+2);
        // -
        System.out.println(3-1);
        // *
        System.out.println(3*2);
        // /
        System.out.println(16/3);
        // %
        System.out.println(16%3);
        //如何由小数参与以上运算，结果有可能不准，原因待解释
```
- 隐式转换
取值范围小的数值向取值范围大的数值转换；（byte<short<int<long<float<double）
byte、short、char 在参与运算时，都会先直接提升为int ，然后进行运算。
- 强制转换
格式：目标数据类型 变量名=（目标数据类型）被强制转换数据
- 字符+数字 ，会先把字符转换成对应的数字在相加（如 'a' 对应的时97，'A'对应的是65）
2. 自增自减运算符
3. 赋值运算符
4. 关系运算符
5. 逻辑运算符
- ^  逻辑异或，相同为false,不同为true
- 短路逻辑运算符（&&,||），效果和&,| 一样，但是具有短路效果
6. 三元运算符
7. 补码和反码
## 二、判断和循环
1. 回文数
```java
        Scanner sc= new Scanner(System.in);
        System.out.println("请输入一个数字");
        int x=sc.nextInt();//赋值一个数字
        int number=x;
        int num=0;
        while(number!=0){
           int ge= number%10;
           number/=10;
           num=num*10+ge;
        }
        System.out.println(num==x?"是回文数":"不是回文数");
```
2. 求商和余数（要求不使用乘除和%）
思想：循环实现
```java
      Scanner sc= new Scanner(System.in);
        System.out.println("请输入被除数");
        int x=sc.nextInt();//赋值一个数字
        System.out.println("请输入除数");
        int y=sc.nextInt();//赋值一个数字
        int remainder=0;//余数初始化
        int business=0;//商初始化
        while(x>=y){
        x-=y;
        business+=1;
        remainder=x;
        }
        System.out.println("商:"+business);
        System.out.println("余数"+remainder);
```
3. 逢7过（从任意数字开始报数，如果报的数字包含7或者是7的倍数，就说过;打印1-100之间满足规则的数字）
```java
    for(int num=1;num<=100;num++){
            if(num%7==0||num%10==7||num/10%10==7)//条件判断的条件要充分考虑各种情况
            System.out.println(num);
        }
```
## 三、数组
1. 数组格式
- 完整格式（数据类型[] 数组名=new 数据类型 [] {元素1，元素2}）
- 简化格式 （数据类型[] 数组名={元素1，元素2}）
- 数据类型有double,int,String
2. 数组初始化长度
- 格式： 数据类型[] 数组名 =new 数据类型[数组长度]
3. 二维数组
```java
 //格式:数据类型[][] 数组名=new 数据类型[][] {{元素1，元素2},{元素1，元素2}};
// 简化格式:数据类型[][] 数组名={{元素1，元素2},{元素1，元素2}};
```
4. Arrays
```java
    //toSting() 将数组编变成字符串
    int [] arr={1,2,3,4,5,6,7};
    System.out.println(Arrays.toString(arr))//[1,2,3,4,5,6,7]
    //二分查找法查找元素（前提：数组必须是有序的，且按照升序）
    //如果要查找元素存在，则返回真实索引，否则会返回-1；
        System.out.println(Arrays.binarySearch(arr,2))//1

    //copyOf()拷贝数组
    int[] newArr1=Arrays.copyOf(arr,10);
    System.out.println(Arrays.toString(newArr1));//[1, 2, 3, 4, 5, 6, 7, 0, 0, 0]

    // copyOfRange()拷贝数组指定范围
    int[] newArr2=Arrays.copyOfRange(arr,1,10);
    System.out.println(Arrays.toString(newArr2));//[2, 3, 4, 5, 6, 7, 0, 0, 0]
    //fill()填充数组
    Arrays.fill(arr,50);
    System.out.println(Arrays.toString(arr));//[50, 50, 50, 50, 50, 50, 50]
    //sort 排序 。默认给基本数据类型升序排列 ，底层是使用快速排序
        int[] arr2={1,5,2,3,9,8,4,19};
        Arrays.sort(arr2);
        System.out.println(Arrays.toString(arr2));//[1, 2, 3, 4, 5, 8, 9, 19]
    //sort 降序写法
        Arrays.sort(arr2,(Integer o1,Integer o2)->{return o2-o1})
    //sort降序原理
        Integer[] arr3={1,5,2,3,9,8,4,19};
        Arrays.sort(arr3,new Comparator<Integer> (){
            @Override
            public int compare (Integer o1,Integer o2){
                return o2-o1;
            }
        });
        System.out.println(Arrays.toString(arr3));//[19, 9, 8, 5, 4, 3, 2, 1]
```
## 四、方法
1. 方法概念及用途
- 方法是程序中最小的执行单元;将重复的代码、具有独立功能的代码可以抽取到方法中;方法可以提高代码的复用性和可维护性。
- 方法必须先定义后调用
2. 最简单方法格式：
```java
public static void 方法名（）{
  方法体
}
```
3. 带参数的方法定义和调用
```java
public static 返回值类型 方法名（int number1,int number2）{
  ...
  ...
  return 返回值
}
//注意方法返回值类型 和返回值的类型 是一样的
```
4. 方法的重载
- 同一个类中，方法名相同，参数不同的方法（个数不同，顺序不同，类型不同），与返回值无关。
```java
//买飞机票
   public static void main(String[] args) {
        Scanner sc= new Scanner(System.in);
        System.out.println("请输入机票价格");
        int price=sc.nextInt();
        System.out.println("请输入月份数（1-12）");
        int month=sc.nextInt();
        System.out.println("请输入机票类型（1-头等舱，0-经济舱）");
        int type=sc.nextInt();
        double num=airPrice(price,month,type);
        System.out.println("当前季节机票价格为:"+num);
    }
    public static double airPrice(int price,int month,int  type) {
        if(month>=5 && month<=10){
            if(type==1)//代表头等舱
            {
                return price*0.9;
            }else{
                return price*8.5;
            }
        }else{
            if(type==1)//代表头等舱
            {
                return price*0.7;
            }else{
                return price*0.65;
            }
        }
    }
    //注意事项: 定义有参数的方法时候，传入的参数类型要与方法定义的参数类型一致；
    //方法如果有返回值，接受该方法返回值的变量，要与方法返回值的类型一样

//开发验证码（验证码长度为5，前四位是大小写字母，最后一位是数字）
  public static void main(String[] args) {
        char[] arr= new char[52];
        for(int i=0;i<arr.length;i++){
            if(i<26){
                //添加小写字母
                arr[i]=(char)(97+i);
            }else{
                //添加大写字母
                arr[i]=(char)(65+i-26);
            }
        }
        String result="";
        //随机抽取四个字母
        Random r=new Random();
        for(int i=0;i<4;i++){
            int randomIndex=r.nextInt(arr.length);
            result+=arr[randomIndex];
        }
        //随机抽取一个数字
        int num=r.nextInt(10);
        result+=num;
        System.out.println(result);
    }
```
5. 键盘录入
```java
import java.util.Scanner;
//nextInt()；接受整数
//nextDouble();接受小数
//next();接受字符串
//遇到空格，制表符，回车就停止接受。

//next Line();接受字符串。
Scanner sc=new Scanner(System.in);
int num= sc.nextInt();
```
## 五、面向对象
1. 类和对象是什么
  类是共同特征的描述（设计图），对象是真实存在的具体实例
  ```java
  public class 类名{
    1.成员变量（属性）
    2.成员方法（行为）
  }
  类名 对象名=new 类名（）
  ```
  封装： 对象代表什么，就得封装对应的数据，并提供数据对应的行为。
2. 关键字
- private:是一个权限修饰符；可以修饰成员变量和方法；被private修饰的成员只能在本类中才能访问。针对每一个私有化成员变量，都要提供一个get和set方法，来给成员赋值或者对外提供值。
- this: 可以区别局部变量和成员变量
3. 构造方法
- 如果没有定义构造方法，系统会给出一个默认的无参构造方法。
- 构造方法重载：带参构造方法和无参构造方法，两者方法名相同，参数不同。
- 构造方法在创建对象的时候，由虚拟机自动调用，给成员变量进行初始化。

4. 标准的javabean类
- 构造方法、私有变量get、set生成的快捷方式： alt+INS或者alt +fn +ins
- 插件PTG 利用他来生成标准的javabean
```java
public class HelloWorld {
  private String username;
  private String password;
  private String email;
  private String gender;
  private int age;

     //空参构造方法

  public HelloWorld() {
  }

  //有参构造方法

  public HelloWorld(String username, String password, String email, String gender, int age) {
    this.username = username;
    this.password = password;
    this.email = email;
    this.gender = gender;
    this.age = age;
  }
  //每个私有变量生成 get和set 方法

  public String getUsername() {
    return username;
  }

  public void setUsername(String username) {
    this.username = username;
  }

  public String getPassword() {
    return password;
  }

  public void setPassword(String password) {
    this.password = password;
  }
```
5. 测试案例
```java
//文字版格斗游戏

import java.util.Random;

/**
 * 角色描述
 *
 * @author 20757
 */
public class Role {
private String name;
private int blood;

    public Role() {
    }

    public Role(String name, int blood) {
        this.name = name;
        this.blood = blood;
    }
    /**
     * 获取
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     * @return blood
     */
    public int getBlood() {
        return blood;
    }

    /**
     * 设置
     * @param blood
     */
    public void setBlood(int blood) {
        this.blood = blood;
    }

 public void attack(Role role){
        //产生随机伤害1-20
     Random r= new Random();
     int hpDamage =r.nextInt(20)+1;
     role.setBlood(role.getBlood()-hpDamage);
     if(role.getBlood()>0){
     System.out.println(this.getName()+"挥舞拳头，打了"+role.getName()+"一下，造成了"+hpDamage+"的伤害，目前"+role.getName()+
             "还剩下"+role.getBlood()+"的血量");
     }else{
         System.out.println(role.getName()+"被"+this.getName()+"KO了");
     }
 }
}

-----------------------------------
public class TextFightingGame
{
    public static void main(String[] args) {
     Role r1=new Role("乔峰",100);
     Role r2=new Role("鸠摩智",100);
     while(r1.getBlood()>0&&r2.getBlood()>0){
         r1.attack(r2);
         if(r2.getBlood()>0)
         r2.attack(r1);
     }
    }
}
```
