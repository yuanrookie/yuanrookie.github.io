---
title: java学习之路--基础知识（四）
author: yuansir


summary: java学习之路的笔记总结
categories: Java 笔记
tags:
  - blog
  - hexo
abbrlink: 15
date: 2023-07-12 23：24：05
---
# java基础知识（四）
## 一、面向对象进阶
1. final
 final修饰方法，表示最终方法，不能被重写；final修饰类，表示最终类，不能被继承；final 修饰变量，表示常量，不能被修改。
2. 权限修饰符
 - private :只能在本类中使用
 - 空着不写 ：在本类或者同一个包下的其他类中使用
 - protected : 本类、同一个包中的其他类，不同包下的子类
 - public : 各种情况下都能使用。
 - 使用规则： (成员变量私有，方法公开；如果方法中的代码是抽取其他方法中共性代码，一般也是私有的)
3. 代码块
 - 局部代码块（提前结束变量的生命周期，已经淘汰）
 - 构造代码块（写在构造方法之前；可以把多个构造方法中重复的代码抽取出来；在创建本类对象的时候，会先执行构造代码块在执行构造方法）
 - 静态代码块（static{} ;  随着类的加载而加载，并且自动触发，只执行一次；用于类加载的时候，数据初始化使用）
4. 抽象类/抽象方法
- 抽象方法：将共性的行为（方法）抽取到父类之后，由于每个子类执行的内容是不用一样的，在父类中不能确定具体的方法体，该方法就可以定义为抽象方法（来使子类必须重写该方法）
格式： public abstract 返回值类型 方法名（参数列表）
- 抽象类
格式 publlic abstract class 类名
抽象类不能实例化（不能创建对象）;
抽象类中不一定有抽象方法，有抽象方法的类一定是抽象类。
可以有构造方法（当创建子类对象的时候，给属性进行赋值）
抽象类的子类（要么重写抽象类中所有抽象方法；要么是抽象类）
5. 接口
  接口就是一种规则，是对行为的抽象；接口不能实例化；接口和类之间是实现关系，通过implements关键字实现。
  - 定义一个接口
   public interface 接口名{
   }
   - 接口和类之间是实现关系
  public  class 类名 implements 接口名{}
   - 接口的子类（实现类）
   要么重写接口中所有的抽象方法
   要么是抽象类
   - 注意事项
  接口和类可以单实现，也可以多实现
  public class 类名 implements 接口名1，接口名2{}
  实现类还可以继承一个类的同时，实现多个接口
  public class extends 父类 implements 接口名1 ，接口名2 {}
   - 接口中成员的特点
   成员变量：只能是常量，默认修饰符：public static final
   构造方法：没有
   成员方法：JDk7以前只能定义抽象方法，JDK8开始可以定义有方法体的方法，JDK9开始可以定义私有方法。
   - JDK8以后接口中新增的方法
   允许在接口中定义默认方法，需要使用关键字default修饰---->解决接口升级问题
   格式：
   public default 返回值类型 方法名（参数列表）{}
   注意事项：
   默认方法不是抽象方法，所以不强制被重写；如果重写记得去掉default;
   public 可以省略，default不可被省略
   如果实现了多个接口，多个接口中存在相同的默认方法，子类就必须对该方法进行重写。
   - JDK9以后接口新增的方法
   私有方法定义格式：
  //普通的私有方法，给默认方法服务的
   private 返回值类型 方法名（）{}
// 静态的私有方法，给静态方法服务的
private static void 方法名（）{}
 - 接口多态
      当一个方法的参数是接口时，可以传递接口所有的实现类的对象
```java
public class Main {
    public static void main(String[] args) {
            Dog dog=new Dog("旺财",2);
            Rabbit rabbit =new Rabbit("小白",1);
            dog.eat();
            dog.swim();
            rabbit.eat();
    }
}

 abstract  class  Animal {
    private String name;
    private int age;

    public Animal() {
    }

    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
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

    public abstract void eat();
}
class Dog extends Animal implements Swim{
    public Dog(String name, int age) {
        super(name, age);
    }

    @Override
    public void eat(){
        System.out.println("吃骨头");
    }

    @Override
    public void swim() {
        System.out.println("狗会狗刨");
    }
}
  class Rabbit extends Animal {
    public Rabbit(String name, int age) {
        super(name, age);
    }

    @Override
    public void eat(){
        System.out.println("吃胡萝卜");
    }
}
class Frog extends Animal implements Swim{

    @Override
    public void eat() {

    }

    @Override
    public void swim() {
        System.out.println("青蛙会蛙泳");
    }
}
--------------
//接口类
public interface Swim {
    public abstract void swim();
}

```
6. 设计模式
- 定义：
设计默认是一套被反复使用、多数人知晓的、代码设计经验的总结。目的是为了可重用代码，让代码更容易被他人理解，保证代码可靠性和程序的重用性。
设计模式就是为了实现目的的各种套路。
- 适配器设计模式
 解决接口与接口实现类之间的矛盾问题（当一个接口中抽象方法过多，但是只需要使用其中一部分的时候）
 书写步骤： 编写中间类XXXAdapter，实现对应的接口，对接口中的抽象方法进行空实现，让真正的实现类继承中间类，并重写需要用的方法（为了避免其他类创建适配器类的对象，中间的适配器类要用abstruct进行修饰）

 7. 内部类
 定义： 在一个类的里面，再定义一个类。
内部类表示的事物是外部类的一部分，内部类单独出现没有任何意义。
特点： 内部类可以直接访问外部类的成员，包括私有；外部类要访问内部类的成员，必须创建对象。
应用场景： 汽车的发动机，ArrayList 的迭代器，人的心脏等
- 成员内部类注意点
成员内部类可以被一些修饰符所修饰；在JDK16之前不能定义静态变量，JDK16 开始可以定义静态变量。
获取成员内部类对象方式
方式一：外部类编写方法，对外提供内部类对象
```java
public class Outer{
    public class Inter{

    }
    public void getInter(){
        return new Inter()
    }
}
```
方式二：直接创建
格式： 外部类名.内部类名 对象名=外部类对象.内部类对象
如： Outer.Inner oi=new Outer().new Inner();
- 静态内部类
格式： Outer.Inter oi =new Outer().Inner();
调用方式：
非静态方法：先创建对象，用对象调用
静态方法：外部类名。内部类名.方法名();
- 局部内部类
定义： 将内部类定义在方法里卖弄就叫做局部内部类，类似于方法里面的局部变量。
外接无法直接使用，需要在方法内部创建对象并使用；该类可以直接访问外部类的成员，也可以访问方法内的局部变量。
- 匿名内部类
定义： 隐藏了名字的内部类

格式：
//继承或实现关系
//方法的重写
//创建对象
    new 类名或者接口名（）{
        重写方法；
    }
```java
//注意下面的  Swim()  <---->public class 类名 impeimplements Swim
//把class名删掉，剩下内容就变成一个没有名字的类，这个类想要实现Swim接口，所以需要在类中重写接口里面所有的抽象方法。
new Swim()
{
    @Override
    publick void swim(){
        System.out.println("重写游泳的方法")
    }
};
```

应用场景： 当方法的参数是接口或者类时；以接口为例，可以传递这个接口的实现对象；如果类只使用一次，就可以使用匿名内部类来简化代码
```java
//实现关系
     //整体我们可以理解为Swim接口的实现类对象
        /*
        class Swim1 implements Swim{
            @Override
            public void swim() {
                System.out.println("重写游泳之后的方法");
            }
        }
        * */
        //接口多态
       Swim s= new Swim(){

            @Override
            public void swim() {
                System.out.println("重写游泳之后的方法");
            }
        };
       //编译看左边，运行看看右边的原则
       s.swim();

----------------------------
//继承关系
       method(
               new Animal(){
                   @Override
                   public void eat(){
                       System.out.println("狗吃骨头");
                   }
               }
       );

       public static void method(Animal a){//Animal a=子类对象 多态
           a.eat();
        };
```
