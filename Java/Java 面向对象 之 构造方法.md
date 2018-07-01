
### 面向对象 之 构造方法

功能：

​ 　　**初始化类对象** ，给类对象中的成员变量进行赋值操作

构造方法的格式:

​ 权限修饰符 **类名** (用于初始化的参数列表) {

​ //初始化语句

​ }
```java
/*
public Preson {
    //初始化语句
}
*/
class demo {
    public static void main(String[] args) {
        Person boy = new Person();
        Person girl = new Person("Lily", 16);
        System.out.println("Girl's age is  " + girl.age);
    }
}
class Person {
    String name;
    int age;

    //开始构造方法
    public Person() {
        System.out.println("使用一次无参构造方法");
    }

    public Person(String name, int age) {
        this.name = name;   //用name给成员变量赋值
        this.age = age;     //用age给成员变量赋值
        System.out.println("使用一次有参构造方法");
    }
}
```

Java反编译工具 javap 反编译 .class (字节码文件)

```
​ javap -c -l -private XXX.class

​ -c: 反编译的一个选项

​ -l: 显示行号

​ -private: 显示所有的类和成员

​ XXX.class: 编译之后生产的字节码文件

```
####构造方法中的细节

1. 如果一个类中，没有自定义构造方法，那么Java编译器会在编译的过程中，帮程序员提供一个**无参的构造方法**，供程序员创建对象使用。
2. 构造方法没有返回值，也不需要用void填充位置
3. 构造方法，必须使用类名，有且只有**构造方法**才可以使用类名
4. 如果在类中，自定义了不管是带有参数的构造方法，还是无参的构造方法，那么Java编译器都不会再提供与当前类对应的无参构造方法。

  **注意: 养成习惯，在创建类时，提供与之对应的无参构造方法备用**

5. 构造方法，可以根据实际需求来定义不同类型参数的，不同参数个数的构造方法，来满足实际的使用需要

####补充知识点

​ 在通过new关键字，借助于构造方法，创建对象时，JVM会擦除掉当前对象在内存堆区申请的空间，

​ 使所有的二进制位全部为 0 。所有的成员变量根据其数据类型，表现出不同的 "0" 值

|类型|0值|
:-----: | :--------:
​ byte, short, int |  0
​ long    | 　　0L
​ boolean 　|　false
​ char  　|　 '\0'
​ float   　| 0.0F
​ double  　　|　 0.0

​ 所有的【**引用数据类型** (类，数组，接口，枚举，标注)】全部都是null
