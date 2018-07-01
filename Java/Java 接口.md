### 接口（对行为的抽象，一种模板式设计）

生活中的接口:

USB 插座  网线RJ-45 HDMI VGA(串口) 3.5mm SATA M2 PCI-E DisplayPort Typc-C Lighting
接口用来拓展当前设备功能，如U盘，鼠标，键盘，摄像头，移动硬盘

代码中的接口: 
　　**拓展当前类的功能，或者用来做版本的更新，打补丁**

使用的关键字: 
　　interface 定义接口的关键字,如 UI设计(User Interface) 
　　implements 一个类**遵从**接口的关键字


定义接口的格式:

```java
interface 接口名 {
    //拓展的内容
    //成员变量  和 成员方法
}
```

接口中的**缺省属性**

```java
interface A {
    //成员变量
    int num = 10;           //在接口中的成员变量缺省属性：public static final
    //成员方法
    public void testA();    //在接口中的成员方法缺省属性：abstract
}

interface B {
    public void testB();
}

//使用implements关键字 遵从 接口
class Test implements A, B {            //这里遵从了两个接口，用逗号隔开
    @Override
    public void testA() {
        System.out.println("遵从接口A实现的testA方法");
    }

    public void testB() {
        System.out.println("遵从接口B实现的testB方法");
    }
}

public class Demo {
    public static void main(String[] args) {
        Test t = new Test();

        t.testA();                      //遵从接口，在Test类中实现的接口A中的抽象方法
        t.testB();
        
        System.out.println(Test.num);   //通过接口A调用接口中的static final 修饰成员变量
        System.out.println(t.num);      //通过接口A的 实现类 Test调用接口A中的成员变量
    }
}
```
1\. **在接口中所有的成员变量**缺省属性都是**public static final**，要求在定义成员变量时。直接赋值
　　例如: USB定义规范是就会确定尺寸，网线接口在定义线序就有会规定。
2\. 在接口中成员方法缺省属性都是**public abstract**。这里要求**遵从**接口的类实现这些方法
　　例如： USB接口规定了连接的方式和硬件要求

**注意事项**

1\. 在interface中定义的**缺省属性**为abstract的方法，要求通过implements关键字**遵从**该接口的实现类，必须实现接口中的所有方法
2\. 在interface中定义的成员变量**缺省属性**都是public static final 一旦定义时初始化
就不能重新赋值
3\. 一个类可以**遵从**多个接口，用 逗号 隔开

####补充知识点final 
final 最终，最后的 
final关键字可以用来修饰类，成员变量，成员方法。

final修饰一个类
　　这个类不能被继承
final修饰一个变量
　　这个变量在赋值之后，不能被修改
final修饰一个成员方法
　　这个成员方法不能被**重写**

面试题:
　　Java中的String能不能被继承？
　不能，因为String类使用final修饰的

接口的一个案例：
```java
/*
* 接口案例：
*       生活中的铅笔，一头是铅笔，一头是橡皮
*       铅笔看作是一个类
*       橡皮认为是一个拓展，用接口展示
*/

import java.time.chrono.Era;

interface Eraser {
    int length = 10;            //缺省属性：public,static,final
    public void clear();
}

class Pencil implements Eraser {
    @Override
    public void clear() {
        System.out.println("橡皮是用来磨牙的");
    }

    public void write() {
        System.out.println("隔壁教室下周开始素描");
    }
}
public class Demo {
    public static void main(String[] args) {
        Pencil p = new Pencil();

        p.clear();
        p.write();

    }

}
```
