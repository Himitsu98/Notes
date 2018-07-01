## 继承

**继承是面向对象语言的三大特征之一。**

生活中继承关系:
　　父亲和儿子的关系。

开发中使用的继承:
　　经常用于游戏开发
　　英雄联盟中，所有的人物，都有这些属性：生命值，魔法值/能量，攻击力，法术强度，移动速度，攻击速度，护甲，魔抗。
　　每一个英雄都有以上的属性，但是如果给每一个英雄的类中，都定义一样的内容。会有大量的代码重复，冗余。我们需要进行归纳总结。
　　在游戏开发中，会把大量重复的共有属性，做成一个**基类**。然后让每一个英雄类都来继承于该**基类**，从而获取到**基类**中属性。

### 在代码中使用继承

在Java开发中，用到的继承关键字，extends

如果A类通过extends继承了B类。
就可以这么说：B类是A类的父类，或者说 A类是B类的一个子类

```java
//游戏的英雄类，包含了所有英雄的共有属性和方法
class Hero {
    int blood;
    int power;

    public Hero() {}

    public Hero(int blood, int power) {
        this.blood = blood;
        this.power = power;
    }

    public void D() {
        System.out.println("Flash~~~~~");
    }

    public void F() {
        System.out.println("Fire~~~~~");
    }

    public void test() {
        System.out.println("父类的test方法");
    }
}

//extends关键字，表示Hero类是VN类的父类，或者VN类是Hero的一个子类
class VN extends Hero {
    String name;    //子类特有的成员变量

    public VN() {}

    public VN(String name) {
        this.name = name;
    }

    public void  R() {
        System.out.println("终极时刻");
    }


}


public class Demo {
    public static void main(String[] args) {
        //创建一个Hero类对象
        Hero aHero = new Hero();
        //VN是Hero的一个子类
        VN uzi = new VN();

        //子类对象可以使用从父类继承来的 非私有化成员变量
        uzi.blood = 100;
        uzi.power = 100;
        uzi.name = "简自豪";

        //子类可以使用从父类继承来的 非私有化成员方法
        uzi.D();
        uzi.F();
        uzi.R();

    }
}
```
继承的注意事项：
1\. 父类中的**非私有化**的成员变量和成员方法，继承于该类的子类对象都可以直接使用。
2\. 父类中的**私有化**成员变量和成员方法，不能被子类继承。因为**私有化的成员变量和成员方法只能在类内使用**，子类实例是在类外堆私有化城管变量或方法进行调用，因此报错。
3\. **重点**
　　发现了一个问题，调用子类的构造方法时，也会调用父类的构造方法。

```java
//游戏的英雄类，包含了所有英雄的共有属性和方法
class Hero {
    int blood;
    int power;

    public Hero() {
        System.out.println("父类的构造方法");
    }

}

//extends关键字，表示Hero类是VN类的父类，或者VN类是Hero的一个子类
class VN extends Hero {
    String name;    //子类特有的成员变量

    public VN() {
        System.out.println("子类的构造方法");
    }
}

public class Demo {
    public static void main(String[] args) {
        //VN是Hero的一个子类
        VN uzi = new VN();
    }
}
/*
父类的构造方法
子类的构造方法
*/
```
**解释:**
　　在内存机制中，父类和子类占用同一块内存，只不过子类在父类的基础上增加了自己的部分(属性)。子类是依附于父类的，先有父类再有子类。
　　一个子类对象的产生，必须先调用父类的构造方法产生一个父类实例，然后在这个实例基础上添加自己的部分。

####总结:
　　在继承的关系下，父类中没有私有化的成员变量和成员方法，都可以被子类继承获得，从而使用。但是一旦私有化，这些成员变量和成员方法，子类就无法在使用。

【使用继承的注意事项】
    继承的确可以减少代码的书写，但是，不能为节省代码而继承。必须是真的存在继承关系的情况下，才可以使用继承。例如:
        动物类 Animal
            程序猿/程序媛 Monkey
            SingleDog    Dog

            绿萝 不属于动物，不能使用继承关系。

继承关系下的内存分析图

![继承内存分析图](D:/%E6%BA%90%E7%A0%81/Day12-%E7%BB%A7%E6%89%BF%E5%92%8Cabstract%E6%8A%BD%E8%B1%A1%E7%B1%BB%EF%BC%8C%E9%A1%B9%E7%9B%AE%E7%AC%AC%E4%BA%8C%E8%AE%B2/img/%E7%BB%A7%E6%89%BF%E5%86%85%E5%AD%98%E5%88%86%E6%9E%90%E5%9B%BE.png)

### super关键字

**在Java编译器编译之后，子类的构造方法中，都会被Java编译加上一个父类的无参构造方法， 用于初始化父类的成员变量**

**想法**
　　既然Java编译会自动添加一个无参的父类的构造方法，用于初始化父类的成员变量。这个操作是合情合理。 那么是否可以手动调用父类的构造方法，用于初始化父类的成员变量呢? 而且Java编译只会提供无参数的父类构造方法，有时，我们需要带有参数的父类构造方法。这是Java编 译器无法处理的。

**前提条件**　 
　　但是，父类的构造方法，子类无法继承获得

**解决方案**　　
　　使用super关键字，调用父类方法的关键字 

```javA
class Father {
    int age;
    String name;

    public Father() {}

    public Father(int age, String name) {
        this.age = age;
        this.name = name;

        System.out.println("Father类的带有两个参数的构造方法");
    }

    public void playGame() {
        System.out.println("捕鱼达人");
    }

}

class Son extends Father {
    String hobby;

    public Son() {
        System.out.println("Son类的无参构造方法");
    }

    public Son(String hobby) {
        this.hobby = hobby;
        System.out.println("Son类带有一个参数的构造方法");
    }

    public Son(int age, String name, String hobby) {
        //子类继承于父类而来的非私有化的成员变量
        this.age = age;
        this.name = name;
        //子类自由的成员变量
        this.hobby = hobby;
    }

    public void play() {
        super.playGame();       //使用super关键字调用
        playGame();             //实际上，不用super关键字也可以直接调用
        System.out.println("PUBG");
    }
}

class Demo {
    public static void main(String[] args) {
        Son son = new Son();
        son.play();
    }
}
```

####super关键字的使用注意事项

1\. super关键字可以用来调用父类的成员方法。可用可不用。
2\.**重点**
　　使用super关键字调用父类的构造方法，格式:
　　　　super(实际参数)
　　Java编译器会根据不同的参数类型，来选择不同的父类中的构造方法来使用。
　　如果使用super关键字调用父类的构造方法，要求，**必须在当前代码块的第一行**

```java
class Father {
    int age;
    String name;

    public Father() {}

    public Father(int age, String name) {
        this.age = age;
        this.name = name;

        System.out.println("Father类的带有两个参数的构造方法");
    }

    public void playGame() {
        System.out.println("捕鱼达人");
    }

}

class Son extends Father {
    String hobby;

    public Son() {
        System.out.println("Son类的无参构造方法");
    }

    public Son(String hobby) {
        this.hobby = hobby;
        System.out.println("Son类带有一个参数的构造方法");
    }

    public Son(int age, String name, String hobby) {
        super(age,name);        //使用super关键字调用父类的构造方法        
        //子类自由的成员变量
        this.hobby = hobby;
    }

    public void play() {
        super.playGame();
        playGame();
        System.out.println("PUBG");
    }
}

class Demo {
    public static void main(String[] args) {
        Son son = new Son(16,"Jack","PUBG");
        son.play();
    }
}
```
　　这里的super关键字调用称之为显式调用，一般用于在子类的构造方法中，当需要**选择不用的构造方法**对父类的构造进行一定的初始化时，用super关键字调用父类的构造方法，通过重载进行初始化


3\. this关键字调用构造方法，和super关键字调用父类的构造方法，不能出现在同一个代码块中。原因仍是违反了第二条，第一行原则。
4\. 在子类中，没有通过super关键字显式调用父类的构造方法。那么Java编译会自动补充一个
    无参的父类构造方法， 所以要求: **以后代码中留有一个无参的构造方法备用**


**回顾**
　this关键字调用类内自己的构造方法格式和注意事项
　　1\. this(实际参数) Java编译器会根据参数类型，来选择不同的构造方法。
　　2\. 如果使用this关键字来调用构造方法，要求必须在当前代码块的第一行
　　3\. this调用构造方法时，不能相互调用。

---

### 重写

**问题**

子类从父类中，继承而来的一些成员方法，可能不符合子类的实际情况。
例如：
　　父类的工作方法job 描述的父类是做机械工程师
　　但是子类是 程序猿

**期望** 
　　在代码复杂度允许范围以内，让job方法，更加适合子类的需求。

**重写 Override**
　　子类从父类**继承**而来的方法，根据子类的实际情况，进行重新的书写。以满足子类的实际情况。
```
@Override
```
这种用法称为**注解**
这里Override的功能是开启严格的重写检查
使用@Override之后，要求子类中重写父类方法，要求除了方法体不一样，其他要求完全一样

```java
class Father {
    int age;
    String name;

    public Father() {}

    public Father(int age, String name) {
        this.age = age;
        this.name = name;
    }

    public void job() {
        System.out.println("机械工程师");
    }

}

class Son extends Father {
    public Son() {}

    public Son(int age, String name, String hobby) {
        super(age,name);
    }

    @Override
    public void job() {
        System.out.println("程序员");
    }
}

class Demo {
    public static void main(String[] args) {
        Son son = new Son();
        son.job();
    }
}
```
而且，当父类中没有该方法时，报错        

### 重写和重载的区别

 区别  |            重写            |       重载
:--: | :----------------------: | :------------:
有无继承 | 必须是在**继承**或者**implement**关系下 |  没有继承，是在一个类内的
有无不同 |     方法声明必须一致，方法体可以不同     | 要求方法名一致，参数必须不同
