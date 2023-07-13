---
title: java学习之路--基础知识（三）
author: yuansir


summary: java学习之路的笔记总结
categories: Java 笔记
tags:
  - blog
  - hexo
abbrlink: 15
date: 2023-07-11 21：30：45
---
# java基础知识（三）
## 一、集合（ArrayList）
1. 集合格式
ArrayList<String> 集合名字=new ArrayList<String>()
集合添加的是引用类型或者基本数据类型对应的的包装类（char-->Character;int --> Integer;其他基本数据类型首字母大写）

2. 集合成员方法
- boolean add(E e) 添加元素，返回值代表是否添加成功
- boolean remove(E e) 删除指定元素
- E remove (int index) 根据索引删除指定元素，并返回这个元素
- E set(int index,E e) 修改指定索引下的元素，并返回原来的元素
- E get (int index) 获取指定索引的元素
- int size() 集合的长度
3. 集合案例
- 添加字符串，并进行遍历
```java
   //创建集合
        ArrayList<String> list=new ArrayList<>();
        // ArrayList<Integer> list =new ArrayList<>()
        //添加元素
        list.add("abvcf");
        list.add("123");
        list.add("sdaw2");
        //遍历集合
        StringJoiner sj=new StringJoiner("--","[","]");
        for (int i = 0; i <list.size() ; i++) {
            sj.add(list.get(i));
        }
        System.out.println(sj);
```
- 添加对象，并遍历对象的属性
```java
public class Student {
    private String name;
    private  int age;

    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
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
     * @return age
     */
    public int getAge() {
        return age;
    }

    /**
     * 设置
     * @param age
     */
    public void setAge(int age) {
        this.age = age;
    }


}
-----------------------
   Student s1=new Student("王大山",20);
   Student s2=new Student("李飞",22);
   Student s3=new Student("海域",234);

     //创建集合
     ArrayList<Student> list=new ArrayList<>();
     //添加元素
        list.add(s1);
        list.add(s2);
        list.add(s3);
     //遍历
        for (int i = 0; i < list.size(); i++) {
            System.out.println("名字是："+list.get(i).getName()+",年龄是："+list.get(i).getAge());
        }
```
## 二、面向对象进阶
面向对象三大特征  封装（对象代表什么，就得封装对应的数据，并提供对应的数据行为）、继承（当类与类之间，存在相同的内容，并满足子类是父类中的一种，可以考虑使用继承来优化代码）、多态。
1. static
- 被static所修饰的成员变量叫做静态变量，被该类所有对象共享；不属于对象，属于类；随着类的加载而加载，优先于对象的存在；调用方式：类名调用，对象调用。
- 被 static所修饰的成员方法，叫做静态方法。多用在测试类和工具类中；javabean类中很少使用。
javabean类：用来秒速和一类事物的类，如student,teacher,dog等；
测试类：用来检查其他类是否书写正确，带有main方法的类，是程序的入口
工具类：不是用来描述事物的，而是帮我们做一些事情的类。
- 注意事项
静态方法中，只能访问静态。非静态方法可以访问所有。静态方法中没有this关键字。
2. 继承
- 格式
 public class Student extends Person{

 }
 - 优势
  可以把多个子类中重复的代码抽取到父类中，提高代码的复用性。
  子类可以在父类的基础上，增加其他的功能，使子类更加强大。
- 特点：
只能单继承：一个类只能继承一个直接父类；
不支持多继承，但是支持多层继承；
java中所有的类都直接或间接继承于Object类；
子类只能访问父类中非私有的成员。
- 子类到底可以继承父类中的哪些内容？
误区一： 父类私有的东西，子类就无法继承？
错误：父类中成员变量，子类可以全部继承，但是对于父类中私有的成员变量 子类无法调用。
误区二：父类中非私有的成员，就被子类继承下来了？
错误：只有父类中的虚方法（非private,非static,非final）才能被子类继承。
- 继承中：成员变量的访问特点： 就近原则。
- 继承中：成员方法的访问特点： 直接调用满足就近原则。
- 方法的重写
 在继承中，子类出现与父类中一摸一样的方法声明，就称子类这个方法是重写的方法；
 可以在子类方法前面加上 @Override 来检验；
只有被添加到虚方法表中的方法才能被重写。
- 继承中： 构造方法的访问特点：
子类中所有的构造方法默认先访问父类中的无参构造，在执行自己。
原因：子类在初始化的时候，有可能使用父类中的数据，如果父类没有完成初始化，子类将无法使用父类的数据。
子类在初始化之前，一定要调用父类构造方法先完成父类数据空间的初始化。
如果想调用父类中的有参构造，必须在第一行手动写super进行调用。
3. 多态
- 应用场景：比如学校管理系统，注册页面（学生，教师，管理员）
- 定义： 同类型的对象，表现出不同的形态。
- 形式： 父类类型 对象名称=子类对象；
- 多态的前提
 有继承关系；有父类引用指向子类对象；有方法重写；
- 多态好处： 使用父类型作为参数，可以接受所有子类对象
```java

public class Main {
    public static void main(String[] args) {
    //创建对象（多态方式）
      Animal a= new Dog();
      //调用成员变量；编译看左边，运行也看左边
        //编译看左边：javac在编译代码的时候，会看左边的父类中是否有这个变量，有，则编译成功，否则失败
        //运行也看左边;java运行代码，实际获取的是左边父类中的成员。
        System.out.println(a.name);//动物
        //调用成员方法：编译看左边，运行看右边
        a.show();
    }
}
class Animal{
    String  name="动物";
    public void show(){
        System.out.println("Animal------show方法");
    }
}
class Dog extends Animal{
    String name="狗";
    @Override
    public void show(){
        System.out.println("Dog-----show方法");
    }
}
class Cat extends Animal{
    String name="猫";
    public void show(){
        System.out.println("Cat-----show方法");
    }
}
```
- 多态优势：
  定义方法的时候，使用父类型作为参数，可以接受所有子类对象，体现多态的扩展性与便利。
  在多态形势下，右边对象可以实现解耦合，便于扩展和维护。
- 多态弊端：
不能使用子类的特有功能。（解决方式： 可以转换成真正的子类类型，从而调用子类独有的功能；转换类型与真实类型不一致会报错）
- 练习案例
```java

public class Main {
    public static void main(String[] args) {
    //创建对象（多态方式）
      Animal a= new Dog();
      Animal b= new Cat();
      Person c=new Person("老王",30);
      c.keepPet(a,"骨头");
      Person d=new Person("老李",25);
      d.keepPet(b,"鱼");
    }
}

    class Person {
        String name;
        int age;
        public Person(String name,int age){
            this.name=name;
            this.age=age;
        }
        public  void keepPet(Animal a,String something) {
           //在这里进行强转  如果a 是 狗 ，就强转成 d
            if(a instanceof Dog d) {
                System.out.println("年龄为" + age + "岁的" + name + "养了一只" + a.getColor() + "的" + a.getName());
                System.out.println(a.getAge() + "岁的" + a.getColor() + "的" + a.getName() + a.eat(something));
            d.lookHome();
            }
        }
    }
class Animal{
    String  color;
    String name;
    int age;

    public Animal() {
    }

    public String eat(String something){
       return something;
    }
    public String getColor() {
        return color;
    }
    public void setColor(String color) {
        this.color = color;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }

}
class Dog extends Animal{
    String  color="黑颜色";
    String name="狗";
    int age=2;

     public Dog(String color, String name, int age) {
        this.color = color;
        this.name = name;
        this.age = age;
    }
    @Override
    public String eat(String something){
        return "侧着头吃"+something;
    }
    public void lookHome(){
        System.out.println("狗在看家");
    }
    public String getColor() {
        return color;
    }
    public void setColor(String color) {
        this.color = color;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
}
class Cat extends Animal{
    String  color="灰颜色";
    String name="猫";
    int age=3;

    public Cat() {
    }

    public Cat(String color, String name, int age) {
        this.color = color;
        this.name = name;
        this.age = age;
    }

    @Override
    public String eat(String something){
        return "两只前腿死死的抱住"+something+"猛吃";
    }
    public void catchMouse(){
        System.out.println("猫在逮老鼠");
    }
    public String getColor() {
        return color;
    }
    public void setColor(String color) {
        this.color = color;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
//注意事项，多态如何强转
        ((Dog) a).lookHome(); //强制类型转换（没有改变原数据类型）
        a.lookhome();
}
```
