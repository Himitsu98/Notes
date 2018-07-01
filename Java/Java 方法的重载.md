### 方法的重载

​ reload

​ 方法/函数重载：

​　　编译器中并不关注数据名称，只关注数据类型。为了简化方法/函数的命名。例如：构造方法功能是一致的，用同一个类名来做为方法名，只是通过参数的类型来区分不同的方法。在Java中，同名方法，只能通过不同的参数来区分彼此，这个称之为**方法的重载**。

```java
class Player {
    private String player;
    private int id;


    public Player() {}

    public Player(String name) {
        this.name = name;
    }

    public Player(int id) {
        this.id = id;
    }
}
```
​ 方法的重载条件:

​ 　　**必要条件: 同名方法, 不同参数类型，同一个类内**
　　  
​ 　　其他条件: 返回值可以相同，可以不同
