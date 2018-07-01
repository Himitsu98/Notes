### 面向对象三大特征之一封装

​ 面向对象语言的三大特征：

​ **1\. 封装**

​ **2\. 继承**

**3\. 多态**

问题:
　　代码中，程序只会严格执行语法规范，进行严格的数据类型检查。只要操作过程中，数据类型没有任何问题，代码就可以执行。但是年龄和性别 不可能出现和生活实际情况不符。
　　因此我们希望，代码中的操作可以首先符合语法规范，同时也要符合生活实际

思考:
　　目前情况下，对于成员变量的赋值操作，很简单方便，但是存在诸多隐患。能否对这种操作进行约束

####封装思想

权限修饰符:
　　public: 公开的，公共的，使用public修饰的成员变量和成员方法，在类外可以借助于类对象直接调用。
　　private: 私有的。如果用private修饰的成员变量或者成员方法，只能在类内使用，类外无法调用。
　　用private修饰的成员变量和成员方法，在类外无法使用。无法给成员变量进行赋值操作，我们该如何进行赋值?

　
**解决问题的方案 setter 和  getter 方法**
　　setter 方法是提供给**类外**用于设置**私有化private修饰的成员变量**
```java
void set成员变量名(){}
```

```java
public void setAge(int a) {
    age = a;
}
```
　　getter 方法是提供给**类外**用于获取**私有化private修饰的成员变量**对应的数据
```java
对应的返回值类型 get成员变量名() {}
```
```java
public int getAge() {
    return age;
}
```
**问题:**
    虽然进行了封装，而且使用了setter和getter去操作成员变量，但是还是没有对赋值操作的数据进行
    约束和判断

**解决问题**
    在setter方法中，对于进行赋值的数据做判断，约束，把不符合实际要求的数据进行删除

```java
 public void setAge(int a) {
     if (a > 0 && a <= 80) {
         age = a;
     } else {
         age = 16;
     }
 }

 public void setGender(char g) {
     if ('男' ==g || '女' == g) {
         gender = g;
     } else {
         gender = '女';
     }
  }
```
**封装的好处**
　　1\. 提高了代码的安全性
　　2\. 简化数据赋值操作，不需要考虑具体实现，使用即可
　　3\. 可以隐藏一部分代码


```java
class Person {
    //成员变量
    private String name; //姓名
    private int age;     //年龄
    private char gender; //性别

    //构造方法
    public Person() {}


      setter方法要求格式为:
          set成员变量名(对应的参数)

    public void setAge(int a) {
        if (a >= 0 && a <= 80) {
            age = a;
        } else {
            age = 16;
        }
    }

    /*
     getter方法要求格式为:
         对应的返回值类型  get成员变量名()
     */
    public int getAge() {
        return age;
    }

    public void setName(String n) {
        name = n;
    }

    public String getName() {
        return name;
    }

    public void setGender(char g) {
        if ('男' == g || '女' == g) {
            gender = g;
        } else {
            gender = '女';
        }
    }

    public char getGender() {
        return gender;
    }

    //成员方法
    public void PUBG() {
        System.out.println("Winner winner chicken dinner!!!");
    }
}

public class Demo {
    public static void main(String[] args) {
        Person p = new Person();

        //p.name = "骚杰";
        //p.age = -5;
        //p.gender = '狗';
        p.setName("骚杰");
        p.setAge(-5);
        p.setGender('狗');

        System.out.println("Name:" + p.getName() + " Age:" + p.getAge()
                + " Gender:" + p.getGender());

        p.PUBG();
    }
}
```


### 构造方法和成员方法的区别

区别  |                        构造方法                         |                  成员方法
:-: | :-------------------------------------------------: | :-------------------------------------:
返回值 |                构造方法没有返回值，也不需要用void占位                | 必须有返回值，如果确实没有需要返回的数据，用void占位，表示该方法没有返回值
方法名 |               构造方法的名字必须和类名一致，不能是其他的名字               |        要符合标识符规范，见名知意，动宾结构，不能使用类名
作用  |                构造方法是用来初始化对象，初始化成员变量                 |            是根据实际需求，来完成不同的功能
调用者 | 构造方法的真实调用者是JVM，通过new关键字在内存堆区创建对象，借助于构造方法，初始化对象中成员变量 |    成员方法目前是通过类对象来调用的，后期会遇到用【类名】调用的方法
