---
title: java学习之路--java常用API
author: yuansir


summary: java学习之路的笔记总结
categories: Java 笔记
tags:
  - blog
  - hexo
abbrlink: 14
date: 2023-07-13 22：20：45
---
# java中常用的API方法
## 一、Math
```java
public static int abs(int a)  //获取参数绝对值
public static int ceil(double a)  //向上取整
public static int floor(double a)  //向下取整
public static int max(int a,int b)  //求最大值
public static int pow(double a,double b)  //返回a的b次幂的值
public static int random()  //获取double类型随机数，[0.0,1.0)
public static int round(float a)  //四舍五入
public static int sqrt(int num)  //开平方
```
## 二、System
- 时间原点： 1970年1月1日 0：0：0 (我国在东8区，有八小时时差)
```java
 public static void exit(int status) //结束java虚拟机  0-正常停止  非0--异常停止
 publick static long currentTimeMills() //获取当前时间的毫秒值\
 publick sttaic void arrayCopy(数据源数组，起始索引，目的数组，起始索引，拷贝个数)  拷贝数组

 ```
 ## 三、Object
 - 顶级父类中只有无参构造方法；
 ```java
 //Object成员方法
  public String toString()  //转换成字符串
  public boolean equals(Object obj) 比较两个对象是否 相等
  protected Object clone(int a) 对象克隆

 ```
 ## 四、正则表达式
1. 基本知识
//字符类（只匹配一个字符）

| 字符类  | 含义 |
| ----| -----|
| [abc]   | 只能是a,b或者c|
| [^abc]| 除了a,b,c之外的任意字符|
| [a-zA-Z]| a到z,A到Z|
| [a-d [m-p]] | a到d 或 m到p|
|[ a-z && [def]]| a-z 和def的交集，即d,e,f|
| [a=z&& [^bc]]| a-z和非bc的交集|
| .|  任何字符|
| \d| 一个数字[0-9]|
| \D|非数字[^0-9]|
| \s| 一个空白字符[\t\n\x0B\f\r]|
| \S|非空白字符 [^\s]|
| \w| [a-zA-Z_0-9]|
|\W| [^\w] 一个非单词字符|
| X?| X,一次或者0次|
| X*|X,0次或者多次|
| X+| X,1次或者多次|
|X{n}| X，正好n次|
|X{n,}| X，至少n次|
| X{m,n}| X，至少m,但不能超过n次|
|(?i)| 忽略后面字符的大小写|
| ?|代表前面的数据|
| ？=| 获取前面的数据|
| ？:| 获取所有数据 |
| ？！| 获取不是指定内容的前面部分 |
| \ \组号| 表示把第几组的内容再出来用一次|
| $组号| 正则外面使用的，代表那一组的数据  |

//非贪婪爬取，尽可能少的获取数据 ，如 +？    *？
//贪婪爬取 ，尽可能多的获取数据 如+   *

// public boolean mathes(String regx)：判断是否与正则表达式匹配，匹配返回true
// 注意\\等价于\
// \转义字符，会改变后面字符的含义

```java
//匹配多个字符
    //以字符串形式打印一个双引号
        System.out.println("\"");
        //表示字母数字下划线组成的的单词长度至少为6
        System.out.println(
                "54d5asd".matches("\\w{6,}")
        );
```
2. 校验手机号
```java
String regx="1[3-9]\\d{9}";
```
3. 验证邮箱
```java
String regx="\\w+@[\\w&&][^_]]{2,6}.[a-zA-Z]{2,3}{1,2}"
```
4. 验证身份证
```java
        //身份证简单校验
        String regx="[1-9]\\d{16}(\\dXx)";
        //身份证复杂校验
        String regx="[1-9]\\d{5}(18|19|20)\\d{2}(0[1-9]|1[0-2])(0[1-9]|[12]\\d|3[01])\\d{3}[\\dXx]"
```
5. 爬虫
```java
    public static void main(String[] args) {
        //爬取字符串中的所有的JavaXX
        String str = "JavaXX双卡单卡圣诞节,dsada+5585,Java12刷卡的话！！！Java14啥的回家啊我顶我顶,Java10等级考试亲爱是" +
                "都会撒谎的教案设计的t贺卡收到水水水水水水水水水水Java15,{sdasd}sdasdadJava2ds";

        //获取正则表达式对象
        Pattern p= Pattern.compile("Java\\d{0,2}");
        //获取文本匹配器的对象
        Matcher m= p.matcher(str);
        //利用循环获取
        while (m.find()){
            String s=m.group();
            System.out.println(s);
        }
        //结果
        //  Java
        //  Java12
        //  Java14
        //  Java10
        //  Java15
        //  Java2
    }
    private static void method(String str) {
        //Pattern:表示正则表达式
        //Matcher: 文本匹配器，作用按照正则表达式规则去读取字符串，从头开始读取。
        //在大串中去找符合规则的子串。

        //获取正则表达式对象
        Pattern p= Pattern.compile("Java\\d{0,2}");
        //获取文本匹配的对象
        Matcher m= p.matcher(str);
        //拿着我呢本匹配器从头开始读取，寻找是否有满足规则的子串
        //没有，返回false
        //有，就返回true.在底层记录子串的起始索引和结束索引+1
        boolean b=m.find();
        //方法底层会根据find方法记录的索引进行i字符串的截取
        //subString(起始索引，结束索引);包头不包尾
        //会把截取的小串进行返回
        String s1=m.group();
        System.out.println(s1);
        //第二次在调用find时候，会继续读取后面的内容，
    }
```
5. 分组
- 定义： 分组就是一个小括号
- 捕获分组（ 就是把这一组的数据捕获出来，再用一次）
```java
     //需求1 判断一个字符的开始字符和结束字符是否一致，只考虑一个字符
        //   \\组号，表示把第几组的内容再出来用一次
        String regex1="(.).+\\1";
        System.out.println("a123a".matches(regex1));//true
        System.out.println("&12323&".matches(regex1));//true
        System.out.println("a123b".matches(regex1));//false

        //需求2 判断一个字符的开始部分和结束部分是否一致？可以有多个字符
        String regex2="(.+).+\\1";
        System.out.println("abc123abc".matches(regex2));//true
        System.out.println("!&12323&!".matches(regex2));//false
        System.out.println("123456789123".matches(regex2));//true
        //需求3 判断一个字符串的开始部分和结束部分是否一致？开始部分内每个字符也需要一致
        //举例 aaa123aaa 111789111  &&abc&& abc123abc
        // (.) 把首字母看作一组
        // \\2把首字母拿出来再次使用
        // * 作用于\\2 ，表示后面出现的内容出现0次或者多次
        String regex3="((.)\\2*).+\\1";
        System.out.println("aaa123aaa".matches(regex3));//true
        System.out.println("111789111".matches(regex3));//true
        System.out.println("&&abc&& ".matches(regex3));//true
        System.out.println("abc123abc ".matches(regex3));//false

//案例：口吃替换
// 将字符串： 我要学学编编编程程程程程程程
// 替换为： 我要学编程


    String str="我要学学编编编程程程程程程";
//    $1 表示把第一组的东西，继续拿出来用
  String s1=  str.replaceAll("(.)\\1+","$1");
        System.out.println(s1);
```
- 非捕获分组 :分组之后不需要再用本组的数据，仅仅是把数据括起来
特点：不占用组号
## 五、JDK时间
1.  SimpleDateFormat类（格式化，解析）
```java

   //   public SimpleDateFormat()  默认格式
   //  public SimpleDateFormat(String pattern) 指定格式

        //1.利用空参构造创建SimpleDateFormat对象
        SimpleDateFormat sdf1=new SimpleDateFormat();
            Date d1=new Date(0L);
            String str1=sdf1.format(d1);
        System.out.println(str1); //  1970/1/1 上午8:00
        //2.利用带参构造创建SimpleDateFormat对象，指定格式
        SimpleDateFormat sdf2=new SimpleDateFormat("yyyy年MM月dd日 HH：mm:ss");
        String str2=sdf2.format(d1);
        System.out.println(str2); //1970年01月01日 08：00:00


      //public final String format(Date date) //格式化（日期对象-->字符串）
      //public Date parse(String source)     解析（字符串-->日期对象）
                  //定义一个字符串表示时间
        String str="2023-11-11 11:11:11";
        //1.利用有参构造创建SimpleDateFormat对象 注意：创建对象的格式要跟字符串格式完全一致
        SimpleDateFormat sdf3=new SimpleDateFormat("yyyy-MM-dd HH：mm:ss");
        Date date =sdf3.parse(str);
        //打印毫秒数
        System.out.println(date.getTime());
```
2. Calendar 代表了系统当前时间的日历对象，可以单独修改，获取时间中的年月日
注意： Calendar 是一个抽象类，不能直接创建对象。
```java
       /*
              public static Calendar getInstance()  获取当前时间的日历对象
              public final Date getTime()  获取日期对象
              public final setTime(Date date) 给日历设置日期对象

              public  long  getTimeInMills()  拿到时间毫秒值
              public  void  setTimeInMills(long millis) 给日历设置时间毫秒值

              public int get(int field ) 取日期中的某个字段信息
              public void set(int field ,int value)修改日历的某个字段信息
              public void add(int field ,int amount) 为某个字段增加或者减少指定的值
         * */

//        1. 获取日历对象
        //细节1： Calendar 是一个抽象类，不能直接new,而是通过一个静态方法获取到子类对象
//        底层原理：
//        会根据系统的不同时区来获取不同的日历对象，默认表示当前时间。
//        会把时间中的 纪元，年，月，日，时，分，秒，星期，等等的都放在一个数组当中。
        // 0-纪元，1-年 ，2-月，3--一年的第几周，4-一个月中的第几周，5-一个月的第几天date...16
        //细节2：
        //月份： 范围0-11， 0代表1月
        //星期 ：   1-星期日  2-星期一 ...
        Calendar c=Calendar.getInstance();
        //2，修改日历时间
        Date d=new Date(0L);
        c.setTime(d);
        System.out.println("日历"+c);//日历java.util.GregorianCalendar[time=0,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=31,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=1970,MONTH=0,WEEK_OF_YEAR=1,WEEK_OF_MONTH=1,DAY_OF_MONTH=1,DAY_OF_YEAR=1,DAY_OF_WEEK=5,DAY_OF_WEEK_IN_MONTH=1,AM_PM=0,HOUR=8,HOUR_OF_DAY=8,MINUTE=0,SECOND=0,MILLISECOND=0,ZONE_OFFSET=28800000,DST_OFFSET=0]


        int year=c.get(1);
        int month=c.get(2);
        int date =c.get(5);
        System.out.println(year+","+month+","+date);//1970,0,1
```
3.jdk8时间类
原因： jdk8的代码更加简单，而且更加安全；JDK7多线程环境下会导致数据安全问题
//细节：JDK8新增的时间对象都是不可变的，，如果修改了时间，实际会产生一个新的时间。
```java
   //1. ZoneId  时区
         //获取所有时区名称
//        Set<String > zoneIds= ZoneId.getAvailableZoneIds();
        //获取当前系统的默认时区
        ZoneId zoneId = ZoneId.systemDefault();
        //获取指定的时区
        ZoneId.of("Asia/Pontianak");
//--------------------------------------------------
        //2. Instant  时间戳
        //获取当前时间的Instant对象（标准时间）
        Instant.now();//2023-07-13T10:49:59.338231400Z
        //根据（秒/毫秒/纳秒）获取Instant对象
        Instant instant1 = Instant.ofEpochMilli(0L);//1970-01-01T00:00:00Z
        Instant instant2 = Instant.ofEpochSecond(1L);//1970-01-01T00:00:01Z
        Instant instant3 = Instant.ofEpochSecond(1L, 1000000000L);//1970-01-01T00:00:02Z
        //指定时区
        ZonedDateTime time =Instant.now().atZone(ZoneId.of("Asia/Shanghai"));//2023-07-13T18:49:32.343855900+08:00[Asia/Shanghai]
        //isXxx判断
        Instant instant4=Instant.ofEpochMilli(0L);
        Instant instant5=Instant.ofEpochMilli(1000L);
        //用于时间判断
        //ifBefore: 判断调用者代表的时间是否在参数表示时间的前面
        boolean result1=instant4.isBefore(instant5);//true
        //ifAfter: 判断调用者代表的时间是否在参数表示时间的后面
        boolean result2=instant4.isBefore(instant5);//false
//        Instant minusXxx(long millisToSubtract) 减少时间系列方法
        Instant Instant6=Instant.ofEpochMilli(3000L);//1970-01-01T00:00:03Z
        Instant instant7 = Instant6.minusSeconds(1);//1970-01-01T00:00:02Z
//-----------------------------------------------
        //3. zoneDateTime
        //获取当前时间对象（带时区）
        ZonedDateTime now =ZonedDateTime.now();//2023-07-13T19:05:34.415003500+08:00[Asia/Shanghai]
        //指定时间对象（带时区）
        //年月日时分秒纳秒方式指定
        ZonedDateTime time1=ZonedDateTime.of(2023,10,1,11,12,12,0,ZoneId.of("Asia/Shanghai"));
        System.out.println(time1);//2023-10-01T11:12:12+08:00[Asia/Shanghai]

        //通过Instant +时区的方式指定获取时间对象
        Instant instant =Instant.ofEpochMilli(0L);
        ZoneId zoneId1=ZoneId.of("Asia/Shanghai");
        ZonedDateTime time2=ZonedDateTime.ofInstant(instant,zoneId);
        System.out.println(time2); //1970-01-01T08:00+08:00[Asia/Shanghai]

//        withXxx修改时间方法
        ZonedDateTime time3=time2.withYear(2000);
        System.out.println(time3);//2000-01-01T08:00+08:00[Asia/Shanghai]
//            减少时间
        ZonedDateTime time4=time3.minusYears(500);
        System.out.println(time4);//1500-01-01T08:00+08:05:43[Asia/Shanghai]
       //增加时间
        ZonedDateTime time5=time4.plusYears(200);
        System.out.println(time5);//1700-01-01T08:00+08:05:43[Asia/Shanghai]
        //-----------------------------------
// 4. DateTimeFormatter  用于时间的格式化和解析

        //获取时间对象
        ZonedDateTime t1=Instant.now().atZone(ZoneId.of("Asia/Shanghai"));
        //解析/格式化器
        DateTimeFormatter dtf1=DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss EE a");
        //格式化
        System.out.println(dtf1.format(time));//2023-07-13 21:52:47 周四 下午

//------------------------------------
        //5.LocalDate ，LocalTime,localDateTime

        //获取当前时间的日历对象（包括年月日）
        LocalDate nowDate=LocalDate.now();
        System.out.println(nowDate);//2023-07-13
        //获取指定的时间的日历对象
        LocalDate ldDate=LocalDate.of(2023,1,1);
        System.out.println("指定日期"+ldDate);//指定日期2023-01-01

//        get系列方法获取日历中的每一个属性值
        //获取年
        int year=ldDate.getYear();
        //获取月
        Month m=ldDate.getMonth();// 或者
        int month=ldDate.getMonthValue();
        //获取日
        int day=ldDate.getDayOfMonth();
        //获取一年的第几天
        int dayOfYear =ldDate.getDayOfYear();
        System.out.println("dayofyear" +dayOfYear);//dayofyear1
        //获取星期
        DayOfWeek dayOfWeek=ldDate.getDayOfWeek();
        System.out.println("dayOfWeek"+dayOfWeek);//dayOfWeekSUNDAY
//        is开头的方法表示判断

        System.out.println(ldDate.isBefore(ldDate));
        System.out.println(ldDate.isAfter(ldDate));
        //with 开头的方法表示修改，只能修改年月日
        LocalDate withLocalDate=ldDate.withYear(1999);
        System.out.println(withLocalDate);//1999-01-01
        //minus 开头的方法表示减少，只能减少年月日，plus相反
        LocalDate minusLocalDate=ldDate.minusYears(100);
        System.out.println(minusLocalDate);//1923-01-01
        LocalDate plusLocalDate=ldDate.plusYears(200);
        System.out.println(plusLocalDate);//2223-01-01


        //工具类
        //duration 时间间隔（秒，纳秒）
        //Period 时间间隔 （年月日）
        //ChronoUnit: 时间间隔 （所有单位）


```
4. 包装类
```java
  1. 利用构造方法获取Integer对象（jdk5之前）
//        Integer i1=new Integer(1);
        //        Integer i4=new Integer(1);
        // System.out.println(i1==i4);//false
//        2. 利用静态方法获取
        Integer i2=Integer.valueOf(127);
        Integer i3=Integer.valueOf((127));
        System.out.println(i2==i3);//true

        Integer i4=Integer.valueOf(128);
        Integer i5=Integer.valueOf((128));
        System.out.println(i4==i5);//false
        //细节：因为再实际开发中，-128——127之间的数据用的比较多，每次都是new一个对象，太浪费内存了，所以提前把这个范围之内的每一个数据都创建好对象，如果用到这个数据，则就返回创建好的对象

```
5. 综合案例练习
```java
   /*
   键盘录入1-100之间的整数，并添加到集合中，直到集合中所有数据总和超过200为止。
   * */
//创建一个集合对象
        ArrayList<Integer>list =new ArrayList<>();
        //键盘录入数据，并添加到集合中
        Scanner r=new Scanner(System.in);
      while(true){
          System.out.println("请输入一个整数");
          String numStr=r.nextLine();
          //将字符串转换为整数
          int num=Integer.parseInt(numStr);
          if(num<1||num>100){
              System.out.println("当前数字不在1-100以内，请重新输入");
              continue;
          }
          //添加到集合中
          //再添加数据的时候，触发了自动装箱，即num自动转换为Integer类型
          list.add(num);
          //统计集合中所有的数据和
          int sum=getSum(list);
          //对sum进行判断
          if(sum>200){
              System.out.println("集合中所有元素的数据和已经满足");
          break;
          }

      }



    private static int getSum(ArrayList<Integer> list) {
        int sum=0;
        for (int i = 0; i <list.size() ; i++) {
            int num=list.get(i);
            sum+=num;
        }
        return sum;
    }
```
