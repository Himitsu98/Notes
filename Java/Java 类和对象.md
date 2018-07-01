### 类和对象

类: 是某些事物的统称，会包含这些事物的属性描述和行为描述 对象: 唯一，独立，特殊的个体

### Java中用代码实现类和对象

在Java中定义类的格式:

```java
class 自定义类名 {
    事物的共有属性描述;
    事物共有行为的描述;
}
```

【注意事项】

```
1\. 类名必须是**大驼峰**命名，要符合标识符规范
2\. 类中只是描述了当前同一类事物的共有属性和方法，但不能确定具体的属性值
3\. 属性的描述称之为【成员变量】，行为的描述称之为【成员方法】
```

代码实现创建一个对象

```java
Scanner sc = new Scanner(System.in)；
```

其中， java.util.Scanner； 是Java中提供的一个扫描器类 利用new Scanner（System.in); 创建了一个扫描器类的类对象

```java
public static demo {
    pubilc static void main(String[] args) {
        /*
        格式：
        类名 类对象 = new 类名();
        类名:自定义的一个数据类型，如Person
        类对象:自定义对象的一个实例，本质是一个引用数据类型
        new :创建对象的关键字
        类名(): 构造方法
        */
        Person p = new Person();
    }
}
```

调用成员变量和成员方法：**. 运算符**

```java
sc.nextInt();
```

这里的.运算符可理解为"的"

```java
p.name = "Jack";
p.age = 16;
p.height = 175;
```

### 类对象内存分析

![类对象内存分析](D:/%E6%BA%90%E7%A0%81/Day08-%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A11.0/img/%E5%AF%B9%E8%B1%A1%E5%86%85%E5%AD%98%E5%88%86%E6%9E%90%E5%9B%BE.png)

### 类对象内存转移问题

```java
class demo {
    public static void main(String[] args) {
        UltraMan Jack = new UltraMan();
        UltraMan Seven = new UltraMan();
        Jack.name = "Jack";
        Seven.name = "Seven";

        Jack.color = "sliver";
        Seven.color = "Red";

        Jack = Seven;

        System.out.println(Jack.name + "'s color is " + Jack.color);
        System.out.println(Seven.name + "'s color is " + Seven.color);
    }
}

class UltraMan {
    String name;
    String color;

}
```
