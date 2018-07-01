## 数组

### 开发中遇到的问题

在代码开发中经常使用大量的相同数据类型的变量，如果按照定义变量的格式，在代码中会出现重 复很多次的语句，而且给这些变量起名也是一个很浩瀚的工程。

1\. 代码中有很多冗余
2\. 变量名都会非常类似，降低阅读性和维护性
3\. 操作不方便，因为变量名非常类似


参考图书馆处理相同图书的方式:

1\. **数据类型一致的**变量放到一起，类似于同一种书籍放到同一个书架上
2\. 给这些数据起一个统一的名字，类似同一种书会有一个统一的编号 T-110
3\. 为了区分不同的个体，给他这些数据一个独立的编号  T-110-01 ~ T-110-05

### 如何定义一个数组

变量定义的格式: 数据类型 变量名 = 初始化数据;

定义数组的格式: 
```java
public static void main(String[] args) {
    数据类型[] 数组名 = new 数据类型[元素个数];
}
```


例如:

```java
int[] arr = new int[10];
        /*
        赋值号左边:
            int: 数据类型，告诉你这个数组中保存的数据是什么类型。这里表示该数组中要保存的数据是int类型
            []: 1\. 告诉你这是一个数组类型数据
                2\. arr是一个数组名，而且是一个【引用】数据类型 【重点知识】
            arr: 数组名，操作数组使用的名字，是一个标识符，要求符合标识符的命名规范
        赋值号右边:
            new: 关键字 "创建数组的关键字"
            int: 数据类型，表示当前数组中保存的数据是int类型
            [10]: 表示该数组【元素个数】为10，数组中可以保存10个int类型的数据。
                有些书籍: 数组的长度，数组的大小，数组的容量~~~
        */

        //还可以这样
        int[] arr = { 1, 2, 3, 4}
        //这样初始化数组时不需要new关键字

        //甚至可以初始化一个匿名数组
        new int[] { 1, 2, 3, 4}
        /*
          这种表示法将创建一个新数组并利用括号中提供的值进行初始化
          数组的大小就是初始值的个数。使用这种语法形式可以在不创建新变量的情况下重新初始化一个数组。
          例如：
          */
        smallPrimes = new int[] { 1, 2, 3, 4}
```

### 如何使用数组

使用数组的格式: 数组名[有效下标];

在计算机世界里，基本上所有的东西都是从0开始的 例如: 元素个数/容量为10的数组，有效下标的范围是0 ~ 9 数组的下标是从0开始到数组的元素个数/容量 - 1 ###数组的内存分析

![数组内存分析](D:/%E6%BA%90%E7%A0%81/Day06-%E6%95%B0%E7%BB%84%E7%AC%AC%E4%B8%80%E8%AE%B2/img/%E6%95%B0%E7%BB%84%E5%86%85%E5%AD%98%E5%88%86%E6%9E%90%E5%9B%BE.png)

#### 数组作为函数的参数

```java
//例如:
//public static void main(String[] args)
import java.util.Scanner;

class Demo5 {
    public static void main(String[] args) {
        int[] array = new int[10];

        System.out.println("请输入10个整数:");
        //一个函数/方法，需要的参数是一个数组类型那么这里只要提供数组名就OK
        getNumbersFromKeyboard(array);

        printIntArray(array);
    }

    /**
    *从键盘上获取int类型数据保存到数组中
    *@param array 传入的用户保存数据的int类型数组
    */
    public static void getNumbersFromKeyboard(int[] array) {
        //参数合法性判断
        if (null == array) {//传入的空间首地址为null
            System.out.println("传入参数不合法");
            return; //结束程序运行
        }

        Scanner sc = new Scanner(System.in);
        //利用for循环，从键盘上获取用户输入的数据
        for (int i = 0; i < array.length; i++) {
            array[i] = sc.nextInt();
        }
    }

    /**
    *展示int类型的数组到命令行
    *@param array 传入的要求展示的int类型数组
    */
    public static void printIntArray(int[] array) {
        //参数合法性判断
        if (null == array) {
            System.out.println("传入参数不合法！");
            return; //结束函数运行
        }

        for (int i = 0; i < array.length; i++) {
            System.out.println("array[" + i + "] = " + array[i]);
        }
    }
}
```

> 与C语言不同，Java中的数组名是**数组类对象的引用类型变量的名字**，我们不关注其是否代表数组第一元素的地址
