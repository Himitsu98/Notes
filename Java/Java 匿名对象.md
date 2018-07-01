### 匿名对象

​ Java中提供了一种使用对象的方式:  **匿名对象**

​ 匿名对象的格式:
```java
​ new 类名(实际参数);
```
​ 用途：

​ 1\. 匿名对象可以用来简化代码的书写，提高效率。

​ 2\. 匿名对象，可以提高内存的利用率，降低没有必要的内存使用。

​ 注意事项：

​ **1\. 匿名对象通常只是用来调用方法 new 类名().成员方法()**
　　当需要调用一次且仅需要调用一次类对象方法时，可以使用匿名对象来调用

​ 2\. 匿名对象不推荐使用成员变量，此时地址未知，成员变量地址丢失
```java
class Person {
    String name;
    int age;

    public Person() {}
    public void playGame() {
        System.out.println("Play PUBG");
    }
}
/* 通过对象来调用
pubilc class Demo {
    public static void main(String[] args) {
        Person p = new Person();

        p.name = "Jack";
        p.age = 16;

        p.playGame;
    }
}
*/
public class Demo {
    public static void main(String[] args) {
        new Person().playGame();
    }
}
```

#### 注意：
　　通常不会使用匿名对象的成员变量，因为无法取出

　　

​ 匿名对象作为方法的参数

​ 文件IO时候会讲

如：BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(new File("C:/aa/1.txt")));
