### main函数浅析

```java
class Demo {
    public static void main(String[] args) {
    }
}
```
public: 权限访问修饰符，最高权限，公开，公共的，main本身就是JVM来调用。使用public是让JVM能够更加方便地操作到当前的main。而main函数是当前Java阶段的程序唯一入口。

static: 静态修饰关键字，调用main不需要任何的对象，直接通过类名调用，甚至于在同一个类中，静态方法调用另一个静态方法时，不需要类名。
实际情况: JVM自己去找类名：
```java
Demo.main(实际参数);
```
void: 没有返回值，main函数比较特殊，调用者是JVM，而JVM不需要main函数的返回值。

main: 特殊的名字，保留关键字。众所周知的名字，在很多语言中，都是使用main函数作为主函数。例如: C / C++

main函数是程序唯一入口(目前阶段)

String[] args: 命令行参数，基本不用。String[] 字符串数组， args，为arguments缩写，表示命令行参数
