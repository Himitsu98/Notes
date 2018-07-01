### 构造代码块

 有时候，我们需要在创建类对象的同时，调用某些方法来进行某些初始化。曾经我们需要在创建类对象之后，
 通过类对象来进行调用，这样并不合理方便
**解决方案**：在构造方法中，调用类内方法，来满足创建对象就调用方法的需求

**瓶颈** ：极端情况下，如果在代码中，有n多个构造方法，如果为了当前需求，也就要与之对应的的创造方法中，
调用n多次方法，这显然不合理。 我们需要一种统一的方式，如果创建了该类的对象，就一定会执行的代码。

**终极解决方案** 构造代码块： { //执行的代码 } 作用: 不管通过哪一个构造方法，创建该类的对象，都会执行构造代码块中代码。 也就是说构造代码块会对【当前类的所有对象】进行初始化

```java
class Baby {
    String name;

    {
        cry();
    }

    public Baby() {}

    public Baby(String name) {
        this.name = name;
        System.out.println("WaAaaaaaaa~");
    }

    public void cry() {
        System.out.println("WaAaaaaaaa~");
    }
}


public class Demo {
    public static void main(String[] args) {
        Baby aBaby = new Baby(); 
    }
}
```
**要求**：构造代码块是放到成员变量之后，构造方法之前

**作用**：
　　不管通过哪一个构造方法，创建该类的对象，都会执行构造代码块中的代码
　　也就是说，构造代码块会对**当前类的所有对象**进行初始化

【代码块】
　　1.构造代码块 
　　2.局部代码块(现在基本不用) 
　　3.静态代码块(后期挺常用)

**Java中，有三种对于成员变量进行赋值操作的方式**

- 定义时初始化
- 构造代码块
- 构造方法

**优先级问题**:
　　 如果类中存在构造方法，那么成员变量初始化的**最终值**由**构造方法**确定 如果只有构造代码块和定义时初始化，谁在后，谁决定成员变量的最终值
```java
class Person {
    int age = 10;

    {
        age = 30;
    }

    public Person() {
        age = 20;
    }
      
}

public class Demo {
    public static void main(String[] args) {
        Person aPerson = new Person();
        System.out.println(aPerson.age);
    }
}
```

### this关键字
```java
class Student {
    private String name;
    private char gender;
    private float score;
    private int age;

    public Student() {}
    public Student(String name, char gender, float score, int age) {
        this.name = name;
        this.gender = gender;
        this.score = score;
        this.age = age;
    }
}
```

**代码中的含义: 
　　表示调用该方法的【对象】本身**
　　
　　在构造方法中，用参数的名字来提是调用者，这里需要的数据是什么，通常情况下，传入参数的名字和成员变量名应是一致的，方便调用者使用。
　　但是，这里由于**就近原则**，在同一个代码块中，出现了同名变量，通常会使用最近的。
　　那么为了确定我们操作的是**类内的成员变量**，这里使用this关键字来借助于 . 点运算符调用**类内的成员变量**和参数的变量进行区分。

```java
class Student {
    private String name;
    private char gender;
    private float score;
    private int age;

    public Student() {}
    public Student(String name, char gender, float score, int age) {
        this.name = name;
        this.gender = gender;
        this.score = score;
        this.age = age;

        System.out.println(this);
    }
}


public class Demo {
    public static void main(String[] args) {
        Student stu = new Student("Jack", '男', 59.9, 18);

        System.out.println(stu);
    }
}
```

**补充**
　　在构造方法中的this关键字，是JVM借助于构造方法，创建出来的类对象。
　　在setter方法中，用this关键字来区分是成员变量还是传入的参数。
　　this关键字可以用来在【类内】调用成员方法 【80%严谨 有漏洞】

### this关键字的特殊用法 【难点】

this关键字可以用来调用类内的方法【80%正确】
　　(没必要，在类中直接使用方法名即可，不需要this)

用this关键字调用【类内的构造方法】

```
格式:
    this(实际参数);
```
```java
class Player {
    private String name;
    private int id;

    public Player() {}

    public Player(String name) {
        //使用this关键字调用构造方法
        //调用无参
        this();
        this.name = name;
    }

    public Player(int id) {
        this("jack")
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }
}

class Demo {
    public void main(String[] args) {


    }
}

```

注意事项：
    1\. Constructor call must be the first statement in a constructor.
    　　在一个构造方法(构造器)调用另一个构造方法，**必须**在整个代码块的第一行
    2\. 在一个构造方法中，只能通过this关键字，调用一个构造方法。(否则违反第一条)
    3\. 两个构造方法，不能通过this关键字相互调用，会导致无限互相调用。
