### static关键字

static 字面含义是静态 

代码中的问题： 
　　发现在代码中，存在某一些成员变量的数据是一样的，例如: Person类的成员变量国籍。每一个对象中都有相同的数据，大量的重复，浪费了过多的数据空间。

考虑： 把这个所有的类对象都要使用的数据，放入到一个共享空间中，供每一个对象使用

解决方法： 使用static关键字修饰成员变量

```java
class Person {
    private String name;

    //使用static修饰的 静态成员变量 ，保存在内存的 数据区
    static String country = "PRC";

    public Person() {}

    public Person(String name) {
        this.name = name;
    }
}



public class Demo {
    public  static void main(String[] args) {
        Person p1 = new Person("花泽香菜");
        Person p2 = new Person("钉宫理恵");
        Person p3 = new Person("日笠阳子");
        Person p4 = new Person("丹下樱");

        System.out.println(p1.country);
        System.out.println(p2.country);
        p2.country = "JP";
        System.out.println(p3.country);
    }
}

/*
PRC
PRC
JP
*/
```

**static关键字使用注意事项:**

1.使用static修饰的成员变量，这些成员变量称之为**静态成员变量**。
　　从内存角度分析，**静态成员变量**实际保存的内存空间，是在内存的**数据区**。不在**类对象**的**堆区**空间内也就是说，这个**静态成员变量**和**类对象**没有 "关系" ,处于不同的内存空间, 类对象只有使用权。
　　从代码运行，生存周期分析，static修饰的**静态成员变量**是在当前文件[.class]加载到内存时，就已经创建，**早于**类对象出现，而类对象被JVM垃圾回收机制收回时，**静态成员变量**仍然存在与内存中

2.用static修饰的**静态成员变量**可以提供给多个类对象使用

3.当真正意义上存在大量的重复数据时，使用static关键字修饰该数据，以达到**节约内存空间，节约资源**的目的。

小问题: 
　　发现通过类对象调用**静态成员变量**，报警告 
```
The static field Person.country should be accessed in a static way.
``` 
　　用static修饰的**静态成员变量**应该用**静态**的方式访问

问题的根源： 
　　用static修饰的成员变量，这个静态成员变量会随着**类文件**在内存中加载时而创建。是**早于**类对象的创建，而且当类对象销毁之后，静态成员变量仍然在内存中存在。所以是**晚于**对象的销毁而销毁。

- 从生存周期的角度分析，静态成员变量保存在内存的**数据区**，而类对象是b保存在内存的**堆区**，**静态成员变量**和**类对象**没有"关系"

- 严格意义来说: 通过对象来调用**静态成员变量**是非法。 Java语言是相对而言非常严谨，这里希望你能够通过一个更加严谨的方式来使用**静态成员变量**。 因为**类对象**和**静态成员变量**没有"关系"，所以他不希望你这么使用。

推荐调用/使用静态成员变量的方式 
```
类名.静态成员变量
Person.country
```
这里没有警告，让你摆脱**类对象**和**静态成员变量**之间的关系。

####修改问题:　　

　　　**静态成员变量**是一个**隐含的共享资源**

　　用static修饰的变量，不管通过哪一个方式修改变量的值，所有用到该**静态成员变量**的地方全部会被修改。因为这个空间是共享的。

```java
class Person {
    private String name;

    //使用static修饰的 静态成员变量 ，保存在内存的 数据区
    static String country = "PRC";

    public Person() {}

    public Person(String name) {
        this.name = name;
    }
}



public class Demo {
    public  static void main(String[] args) {
        //在此之前没有对象
        System.out.println(Person.country);
        Person p1 = new Person("花泽香菜");
        Person p2 = new Person("钉宫理恵");
        Person p3 = new Person("日笠阳子");
        Person p4 = new Person("丹下樱");

        System.out.println(p1.country);
        System.out.println(p2.country);
        p2.country = "JP";
        System.out.println(p3.country);
    }
}
/*
PRC
PRC
PRC
JP
*/
```
###静态成员变量和构造代码块实现计数

静态成员变量的运用：
　　统计一个类被创建了多少次，实际场景：用户ID号，数据统计，访问统计，用户统计

创建用户，ID号随着创建的用户个数，自动递增

需求：
　　1.需要一个持久化的数据，用于保存ID号  
　　2.需要一个赋值操作，把自动生成的ID赋值给每一个VIP对象

持久化问题：
　　可以使用static修饰的静态成员变量

赋值操作：
　　每一个对象都需要被赋值ID号，无论通过哪一个构造方法来创建对象 
　　构造代码快，可以用来初始化当前类的所有类对象

```java
class VIP {
    private String name;
    private int id;
    private char gender;
    //私有化静态成员变量
    /*
    私有化静态成员变量
    1.私有化是为了在类外不能随意访问
    2.静态，保存在内存的数据区，程序只要不退出就会一直存在
     */
    private static int count = 1;

    /*
    构造代码块，用于初始化每一个对象的ID值
     */
    {
        this.id = count++;
    }

    public VIP() {}

    public VIP(String name) {
        this.name = name;
        this.gender = gender;
    }

    //ID是系统自动生成，只提供getter方法

    public int getId() {
        return id;
    }

    public char getGender() {
        return gender;
    }

    public void setGender(char gender) {
        this.gender = gender;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

class Demo {
    public static void main(String[] args) {
        VIP v1 = new VIP();
        VIP v2 = new VIP("Jack");
        VIP v3 = new VIP("Rose");
        VIP v4 = new VIP("Nero");

        System.out.println("v1 : " + v1.getId());
        System.out.println("v2 : " + v2.getId());
        System.out.println("v3 : " + v3.getId());
        System.out.println("v4 : " + v4.getId());
    }
}
```
### static关键字修饰成员方法

static 可以用来修饰成员方法，而修饰的成员方法称之为【静态成员方法】

```java
/*
格式:
权限修饰符  static 返回值类型 方法名(形式参数列表) {
    //方法体
}
*/
```

**重点**

用static修饰的成员方法，称之为**静态成员方法**，这个**静态成员方法**是随着类文件(.class) 加载到内存时加载。**早于**类对象的创建，而当类对象被JVM垃圾回收机制销毁时，**静态成员方法**仍然存在于内存中，所以是**晚于**类对象的销毁而销毁。
**静态成员方法**和**类对象**没有"关系"

```java
class Dog {
    private String name;

    public Dog(String name) {
        this.name = name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public static void sleep() {
        System.out.println("Huluuuuuuu");
    }
}

public class Demo {
    public static void main(String[] args) {
        Dog d1 = new Dog("Harski");
        System.out.println(d1.name);

        Dog d2 = new Dog();
        d2.setName("Samoye");
        System.out.println(d2.name);

        d1.sleep();
    }
}

```

使用类对象来调用静态成员方法会报警告 
```
The static method sleep() in type Dog should be accessed in a static way; 
```
在类内的静态成员方法应该通过静态的方式访问。

这里推荐的调用方式； **类名.静态成员方法();** 让你忘记【对象】和【静态成员变量】有关系

```java
public class Demo {
    public static void main(String[] args) {
        Dog d1 = new Dog("Harski");
        System.out.println(d1.name);

        Dog d2 = new Dog();
        d2.setName("Samoye");
        System.out.println(d2.name);

        Dog .sleep();
    }
}

```

####静态方法运用工具类
静态成员方法的使用：
　　做成工具类，直接使用类名调用，操作简单，不需要对象
　　比如数组操作工具类Arrays
　　在工具类中，所有的方法，需要的参数都是外来数据，和类内的成员变量无关，可视为没有成员变量

**Arrays工具类的几个方法：**
　　sort            快速排序
　　toString        字符串展示
　　binarySearch    二分法查找系统版

```java
import java.util.Arrays;

public class Demo {
    public static void main(String[] args) {
        int[] arr = new int[] {1, 3, 5, 7, 9, 2, 4, 6, 8, 10};

        //利用Arrays工具类中的sort方法，默认结果为号升序
        Arrays.sort(arr);

        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }


        //binarySearch 二分法查找,找到返回一个正数，如没有找到，返回负数
        int index = Arrays.binarySearch(arr, 7);
        System.out.println(index);
        //将数组转为字符串形式返回
        System.out.println(Arrays.toString(arr));
    }
}
```

####封装一个自己的toString方法
```java
ublic class MyArrays {
     /**
      * 此方法将一个数组以字符串的形式返回，格式为:[a, b, c,.....]  ------>{a, b, c,.....}
      * @param arr 需要展示的数组
      * @return  转换后的字符串，返回{}表示运行失败或输入有误
      */
     public static String myToStrings(int[] arr) {
         if (null == arr || arr.length == 0) {
             return "{}";
         }

         String geter = "{";

         for (int i = 0; i < arr.length; i++) {

             if (i != arr.length - 1) {
                 geter += arr[i] + ", ";
             } else {
                 geter += arr[i] + "}";
             }

         }

         return geter;
     }
}

```
####注意事项

1. 在static修饰得**静态成员方法**中，不能使用this关键字

  结果推论：
  　　因为**静态成员方法**有两种调用方式，一种是通过**类对象**，一种是通过**类名**
  但是通过**类对象**调用**静态成员方法**是会报警告的。this关键字表示的是调用
  该方法的类对象，但是这里存在使用类名调用**静态成员方法**的方式。使用类名调用
  该方法是**没有对象**。因此为了避免错误，一律不能使用this关键字。


  原理推论:
  　　因为**静态成员反复**是**早于**类对象的创建而加载，**晚于**类对象的销毁而销毁、
  和类对象没有"关系"。就算没有类对象，这个方法仍然存在。这里**没有对象**。所以
  不能使用this关键字
  

  ​ 　　　**static修饰的方法内部不允许出现非静态成员变量或成员方法，
  　　　即static修饰的方法与该类相关，但是跟该类的具体实例无关**


2. 在static修饰的静态成员方法中，不能使用非静态成员变量，因为非静态成员变量是随着类对象的创建而保存在**内存的堆区**，但是在没有对象之前，已经可以通过类名来调用静态成员方法，这里操作时没有对象。没有对象，所以不能使用非静态成员变量。

3. 静态成员变量可以在静态成员方法中使用

4. 在静态方法中可以调用当前类或者其他类的构造方法，来创建对象。因为main方法自身就是一个静态方法。

**总结** 
　　**静态对静态，非静态对非静态**



####静态成员方法的用途


1\. 调用方便，可以摆脱对象的束缚。
2\. 可以用来完成一些工具类，如Arrays
   


面试题: 类方法能不能使用成员变量？ 
　　答: 类方法可以使用static修饰的成员变量，但是不能直接使用普通的非静态成员变量。

- 一个方法，如果不加static关键字，那么这个方法时属于类实例的，通过一个实例调用

- 如果方法前有static关键字，表示这个方法属于这个类本身，不属于他的任何实例，可以不通过实例调用，并且所有的实例都共享这一个方法，对方法的调用各个实例相互可见。


**知识补充:**
    类方法: 是通过类名调用的方法，称之为类方法。**静态成员方法**
    类变量: 是通过类名调用的成员变量，称之为类变量，**静态成员变量**
