### 多态

**父类的引用指向子类的对象，或者是接口的引用指向遵从接口的类对象，这就是多态**

```java
Human aMan = newMan(); 父类的Human引用了指向子类Man的aMan对象

interface test{}

class test1 extends test{}

test t = new test(); //错误

test t = new test1(); //正确

```

指允许不同类的对象对同一信息做出响应。即同一信息可以根据发送对象的不同而采用多种不同的行为方式。

```java
/*
* 一个动物园：
*   Animal:
*       Monkey
*       Tiger
*       Panda
*
*       给动物喂食物
*
* 发现：
*      每一个类中，都有与之对应的eat方法，而且方法一致，名字相同
*
* 思考：
*      能不能写一个喂动物的方法，传入的对象可以是不同的子类
*
* 尝试：
*      在Animal类中，定义一个喂食的方法，传入的参数为Animal
*
* 发现：
*       在一个方法中，需要的是Animal类的对象作为参数，但当我们传入的是Aniamal类的子类对象时，也没有报错
*
*       从语法角度分析，这里就是父类的引用，指向子类的对象，即多态
*
* 好处：
*       1.一个方法参数利用多态，可以拓宽传入的数据范围，传入的数据包括当前类的直接子类和间接子类
*       2.一个方法返回值利用多态，可以拓宽返回的数据范围，返回的数据可以是当前类对象，也可以是当前类的子类对象，或者间接子类对象
*/

class Animal {
    int age;

    public Animal() {}

    public Animal(int age) {
        this.age = age;
    }

    public void eat(Animal a) {
        System.out.println(a.getClass() + "吃饭了");
    }

    public static Animal tellWhoAreYou(Animal a) {
        System.out.println(a.getClass());
        return a;
    }
}

class Monkey extends  Animal {
    public void eat() {
        System.out.println("猴子吃香蕉");
    }
}

class CodingMonkey extends  Monkey {

}

class Tiger extends  Animal {
    public void eat() {
        System.out.println("老虎吃鸡");
    }
}

class Panda extends  Animal {
    public void eat() {
        System.out.println("熊猫吃竹子");
    }
}

class Demo {
    public static void main(String[] args) {
        Monkey m = new Monkey();
        Tiger t = new Tiger();
        Panda p = new Panda();

        Animal a = new Animal();
        a.eat(m);
        a.eat(t);
        a.eat(p);

        a.eat(new CodingMonkey());

        Animal.tellWhoAreYou(new Tiger());
        Animal.tellWhoAreYou(new Monkey());
        Animal.tellWhoAreYou(new Panda());
        Animal.tellWhoAreYou(new CodingMonkey());

        //正确
        Animal aAnimal = Animal.tellWhoAreYou(new Tiger());
        //错误
        //Tiger aAnimal = Animal.tellWhoAreYou(new Tiger());

        //正确,强制类型转换，把大数据类型转换为小数据类型
        Animal t1 = (Tiger)Animal.tellWhoAreYou(new Tiger());
        Monkey m1 = (Monkey) Animal.tellWhoAreYou(new Tiger());
        Panda p1 = (Panda) Animal.tellWhoAreYou(new Tiger());
        CodingMonkey c1 = (CodingMonkey) Animal.tellWhoAreYou(new Tiger());


    }

}
```
**多态使用注意事项：**

```java
class Animal {
    int num = 1;
    static int  age = 1000;

    public void eat() {
        System.out.println("动物吃饭");
    }

    public static void sleep() {
        System.out.println("动物睡觉");
    }

    public void run() {
        System.out.println("动物跑");
    }
}

class Cat extends  Animal {
    int num = 10;
    static int age = 10;
    String name = "Caffee";

    public void eat() {
        System.out.println("猫吃猫粮");
    }

    public static void sleep() {
        System.out.println("猫睡纸箱");
    }

    public void catchMouse() {
        System.out.println("猫抓老鼠");
    }
}

public class Demo {
    public static void main(String[] args) {
        Animal am = new Cat();

        am.eat();
        am.sleep();
        am.run();

        //am.catchMoutse();                //报错
        //System.out.println(am.name);     //报错
        System.out.println(am.num);
        System.out.println(am.age);
    }
}
/*
猫吃猫粮
动物睡觉
动物跑
1
1000
*/
```
1\. 多态情况下，父类的引用调用父类和子类同名的普通成员方法，那么调用的是子类的方法
2\. 多态情况下，父类的引用调用父类和子类同名的普通成员变量，那么调用的是父类的成员变量
3\. 多态情况下，父类的引用调用父类和子类同名的**静态**成员方法，那么调用的是父类的**静态方法**，
　　　　容易出错，不推荐这么用。
4\. 多态情况下，父类引用不能调用子类特有的成员变量和成员方法

###接口的引用指向遵从接口的类对象

```java
/*
USB接口案例
 */
interface  USB {
    //要求所有的USB设备，都要完成连接方法
    public void connect();
}

//UPan类遵从USB接口i，实现其connect方法
class UPan implements USB {
    @Override
    public void connect() {
        System.out.println("U盘连接电脑传输数据");
    }
}


class KeyBoard implements USB {
    @Override
    public void connect() {
        System.out.println("键盘连接电脑输入数据");
    }
}

class Filco extends KeyBoard {
    @Override
    public void connect() {
        System.out.println("Filco蓝色陶瓷面");
    }
}

class Mouse implements USB {
    @Override
    public void connect() {
        System.out.println("鼠标我选赛睿");
    }
}

/*
 *电脑上留有一个USB接口，用于连接设备
 *具体USB接口用来干什么，由USB设备来约束，电脑只是使用了USB接口
 */

/**
 * 这里是电脑所有USB接口的方法，传入的参数是USB接口
 * @param usb 要使用的USB接口
 */
class Computer {
    public void USBConnect(USB usb) {
        usb.connect();
    }

}
public class Demo {
    public static void main(String[] args) {
        Computer thinkPad = new Computer();

        //Upan是一个遵从了USB接口的类对象
        UPan sandisks = new UPan();

        //当前电脑对象中，有一个使用USB接口的方法，需要设备连接USB接口
        thinkPad.USBConnect(sandisks);

        //匿名对象作为方法的参数，这里使用一个KeyBoard对象，该对象遵从USB接口
        thinkPad.USBConnect(new KeyBoard());

        thinkPad.USBConnect(new Filco());
    }

}
/*
U盘连接电脑传输数据
键盘连接电脑输入数据
Filco蓝色陶瓷面
*/
```
**要点:**
1. 这里也是多态，接口的引用指向遵从接口的类对象
2. 使用接口作为方法的参数，可以传入的数据为**遵从**接口的类对象，或者**遵从**接口的子类对象
