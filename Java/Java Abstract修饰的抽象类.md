### Abstract修饰的抽象类

游戏开发中，通常会有一个基类，保存所有的游戏人物通用属性和方法。这里方法没有做具体的描述，只是确定一定会有这个方法。但是目前的情况下，父类中已经完成了这些规定的方法书写，子类中可以重写，也可以不重写，这些从语法角度没有任何问题。但是到了实际运行的过程中，我们仍希望可以不需要重写，也不执行父类的方法。

**瓶颈**
　　无法要求子类强制重写代码，以满足子类的特定需求。
**需求**
　　希望能够**强制要求**子类重写父类中要求的方法。做到错误前置

**解决方案**
　　 **abstract**修饰成员方法，这个方法是要求继承于该类的子类，强制**完成**的方法。

```java

abstract class Hero {
    String name;

    public Hero() {
    }

    public Hero(String name) {
        this.name = name;
    }
    /*
     * 以下方法，是要求子类必须按照自己的情况完成，
     * 使用abstract修饰
     * 用abstract修饰的方法， 不需要方法体
     */
    abstract public void Q();
    abstract public void W();
    abstract public void E();
}
class Fizz extends Hero {

    public void Q() {
        System.out.println("淘气打击");
    }

    @Override
    public void W() {
        System.out.println("海石三叉戟");
    }

    @Override
    public void E() {
        System.out.println("古灵精怪");
    }
}

class Jax extends  Hero {
    @Override
    public void Q() {
        System.out.println("穿刺之箭");
    }

    @Override
    public void W() {
        System.out.println("枯萎箭袋");
    }

    @Override
    public void E() {
        System.out.println("恶灵箭雨");
    }
}

class Zed extends Hero {
    public void Q() {
        System.out.println("手里剑");
    }

    public void W() {
        System.out.println("影分身");
    }

    public void E() {
        System.out.println("不知道");
    }
}
public class Demo {
    public static void main(String[] args) {
        Fizz fizz = new Fizz();

        fizz.Q();
        fizz.W();
        fizz.E();

        Zed zed = new Zed();

        zed.Q();
        zed.W();
        zed.E();
    }
}
/*
淘气打击
海石三叉戟
古灵精怪
手里剑
影分身
不知道
*/
```
**abstract关键字使用注意事项**

1. 如果一个方法，用把abstract修饰，那么这个方法就不能有方法体，只有方法的声明，并且用分号结尾。例如:

  ```java
   abstract public void Q();
  ```

2. 一个子类如果继承了一个用abstract修饰的父类，那么就要求子类必须实现在abstract父类中定义的所有abstract方法
3. 如果一个类中存在用abstract修饰的方法，那么这个类必须用abstract修饰。

4. abstract类，不能有自己的类对象。 
解释:
　　因为用abstract修饰的类中，可能包含用abstract修饰的方法。而使用abstract修饰 的方法，是没有方法体。假如用abstract修饰的类有自己的类对象。请问如何调用没有方法体的 abstract修饰的方法?因此，**abstract修饰的类是没有自己的类对象**

5. 一个类中没有abstract方法，这个类用abstract修饰可以吗? 这样做没有必要，语法允许，但是会增加代码的逻辑复杂度。

**总结** 
　　如果一个类继承了用abstract修饰的**抽象类**，那么要求该类必须完成**抽象类**中的所有**抽象方法**
