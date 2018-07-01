## 循环结构

顺序结构 分支结构 循环结构 实际问题: 在代码中，可能存在大量重复功能代码。需要一遍一遍的书写。这样的代码会导致
1\. 代码臃肿
2\. 阅读性极差
3\. 维护性极差


### while循环

```java
while (/*循环条件 true/false*/) {
    //循环体
    //(循环条件变更)
}
/*
执行流程:
    当程序运行到while循环，首先判断循环条件，如果条件为true 执行循环体(循环条件变
    更)。进入下一次循环，直到while 之后的循环条件为false，循环终止!!!
【注意】
    在代码中出现死循环，Ctrl + C 终止程序运行
*/
```

### do - while循环

```java
do {
    //循环体
    //(循环条件变更)
} while (/* 循环条件 true/false */);;;;;;;;;;;;;
/*
执行流程；
    当程序运行到while循环时，不管3721直接运行一次循环体(循环条件变更)，然后再来
    判断while之后的循环条件十分为true， 如果为true执行，下一次循环，如果为false
    终止循环。
*/
```

### while 和 do - while 的区别

while 和 do - while 之间的一个区别是 while循环的每一次执行都是在控制范围以内的，但是do -while循环第一次执行 是不经过任何的判断，就会执行的。 所以这里存在一定的隐患

程序猿/媛生存法则: 【已知】 【可控】 【个人建议】 能用while解决的问题，就不要用do - while

### for循环

```java
for (/*循环条件初始化*/; /*循环条件判断*/; /*循环条件变更*/) {
    //循环体
}
```

### continue关键字

字面含义:继续， go on 在代码中的含义是: 结束当前次循环，直接进入下一次循环

如果将continue语句用于for循环中，就可以跳到for循环的"更新"部分

**注意**
1\. 在while或者do - while中，如果使用continue关键字，要时刻注意continue
关键字的位置，是否会影响到循环条件变更。如果影响到会导致死循环
2\. for循环中，可以肆无忌惮的使用continue

**建议** 
　　如果业务逻辑中，不得不使用continue关键字，请和for循环配合使用

​ **尽可能不使用 continue，如果必须使用，和 for 一起用**

### break关键字

字面含义: 打破 代码中的含义是: 跳出 跳出switch case结构或者循环结构

### 循环练习

```java
//1\. 请展示100以内的所有奇数。
class demo{
    public static void main(String arg[]){
        for(int i = 0; i < 100; i++){
            if (i % 2 == 1){
                System.out.println（i);
            }
        }
        for(int i = 1; i < 100; i += 2){    //这里使用了i+=2，减少了循环次数
            System.out.println(i);
        }
    }
}
//2\. 展示100以内除了所有7的倍数和含有7的数以为的所有数
class demo{
    public static void main(String arg[]){
        for(int  i =0; i < 100; i++){
            if((i % 10 == 7) || i % 7 == 0 || i % 10 == 7){
                System.out.println("过")；
            }else{
                System.out.println(i)；
            }
        }
    }
}
//3\. 模拟点菜 利用循环和分支结构 存在的问题是循环次数不确定
    import java.util.Scanner;
    class demo{
        public static void main(String arg[]){
            int choose = 0;//保存用户输入的信息
            Scanner sc = new Scanner(System.in);
            do{
                System.out.println("1.红烧肉");
                System.out.println("2.红烧鱼");
                System.out.println("3.红烧排骨");
                System.out.println("4.红烧肥肠");
                System.out.println("5.酱牛肉");

                switch (choose) {
                    case 1:
                        System.out.println("1.红烧肉");

                        break;
                    case 2:
                        System.out.println("2.红烧鱼");
                        break;
                    case 3:
                        System.out.println("3.红烧排骨");
                        break;
                    case 4:
                        System.out.println("4.红烧肥肠");
                        break;
                    case 5 :
                        System.out.println("5.酱牛肉");
                        break;
                    case 6:
                        System.out.println("点完了");
                        break;
                    default:
                        System.out.println("要来点什么？");
                        break;
                }
            }while(choose != 6);
        }
    }
4\. /*打印出如下图形：
           *****
           *****
           *****
          *****
           *****
   */
    import java.util.Scanner;
    class demo{
        public static void main(String args[]){
            int length;        //接收长度
            System.out.println("你想要的长度是？");
            Scanner scl = new Scanner(System.in);
            length = scl.nextInt();     //利用nextIn()函数获取输入的整数赋值给length
            int high;        //接收宽度
            System.out.println("你想要的高度是？");
            Scanner sch = new Scanner(System.in);
            high = sch.nextInt();        //利用nextIn()函数获取输入的整数赋值给length
            for (int i = 0; i < high ; i++){
                for (int j = 0; j < length; j++){
                    System.out.printf("*");
                }
                System.out.printf("\n");
            }
        }
    }


5\. /*打印出如下图形：
      *
      **
      ***
      ****
      *****
   */
    class demo{
        public static void main(String args[]){
            for (int i = 0; i < 5; i++ ){
                for (int j = 0; j <= i; j++){
                    System.out.print("*");
                }
                System.out.println();
            }
        }
    }
6./*打印出以下图形：
                                    line    block    star
              *        0000*0000            1      4x2      1
             ***      000***000            2      3x2      3
            *****   00*****00            3      2x2      5
           *******  0*******0            4      1x2      7
          ********* *********            5      0x2      9
   */
    import java.util.Scanner;
    class demo{
        public static void main(String args[]){
            int high;     //指定圣诞树高度
            Scanner sc = new Scanner(System.in);
            System.out.println("你想要多高的圣诞树？");
            high = sc.nextInt();

            //程序开始
            int numberOfBlock = high - 1;    //一开始的空格数

            //外层循环控制层数
            for (int  line = 1; line <= high; line++){
                //内层循环控制空格与星星
                int numberOfStar = 2 * line - 1;
                for (int j = 0; j < numberOfBlock; j++){
                    System.out.print(" ");
                }
                for (int k = 0; k < numberOfStar; k++){
                    System.out.print("*");
                }
                for (int j = 0; j < numberOfBlock; j++){
                    System.out.print(" ");
                }
                System.out.println();
                numberOfBlock --;

            }
        }
    }
7./*打印出如下图形：

            *           
           ***
          *****
         *******
        *********
         *******
          *****
           ***
            *
    */
    import java.util.Scanner;
    class demo{
        public static void main(String args[]){
            int high;     //指定圣诞树高度
            Scanner sc = new Scanner(System.in);
            System.out.println("你想要多高的圣诞树？");
            high = sc.nextInt();

            //程序开始
            //打印上半部分
            //外层循环控制层数
            int numberOfBlock1 = high - 1;  
            for (int  line = 1; line <= high; line++){
                //内层循环控制空格与星星

                int numberOfStar = 2 * line - 1;
                for (int j = 0; j < numberOfBlock1; j++){
                    System.out.print(" ");
                }
                for (int k = 0; k < numberOfStar; k++){
                    System.out.print("*");
                }

                System.out.println();
                numberOfBlock1 --;

            }
            int numberOfBlock2 = 1;
            int line2 = high - 1;
            for (int i = high - 1; i > 0; i--){           
                int numberOfStar = 2 * line2 - 1;
                for (int j = 0; j < numberOfBlock2; j++){
                    System.out.print(" ");                 
                }
                for (int k = 0; k < numberOfStar; k++){
                    System.out.print("*");
                }

                System.out.println();
                numberOfBlock2 ++;
                line2--;


            }
        }
    }
//过于繁琐，应尽量减少变量数量，增加可读性，能用一个变量解决就不要用两个
    import java.util.Scanner;
      class demo{
        public static void main(String[] args){
            int high;     
            Scanner sc = new Scanner(System.in);
            System.out.println("你想要多高的圣诞树？");
            high = sc.nextInt();
            //程序开始
            for (int i = 1; i <= high; i++){
                //空格数等于 high - 1
                for (int j = 1; j <= high -i; j++){
                    System.out.print(' ');
                }
                //星星数等于 行数 * 2 - 1
                for (int k = 1; k <= i * 2 -1; k++){
                    System.out.print('*');
                }
                System.out.println();
            }
            //绘制下半部分
            for (int i = 1; i <= high - 1; i++){
                for (int j = 1; j <= i; j++){
                    System.out.print(' ');
                }
                for (int k = 1; k <= 2 * (high - i) - 1; k++){
                    System.out.print('*');
                }
                System.out.println();
            }
        }
    }
    //进行函数封装
    import java.util.Scanner;
    class demo{
        public static void main(String[] args){
            Scanner sc = new Scanner(System.in);
            System.out.println("你想要多高的圣诞树？");
            int high = sc.nextInt();
            printTree(high);
        }
        /**
        *此方法打印出一个圣诞树
        *@param 打印的高度
        */
         public static void printTree(int high){
            //程序开始
            for (int i = 1; i <= high; i++){
                //空格数等于 high - 1
                for (int j = 1; j <= high -i; j++){
                    System.out.print(' ');
                }
                //星星数等于 行数 * 2 - 1
                for (int k = 1; k <= i * 2 -1; k++){
                    System.out.print('*');
                  }
                System.out.println();
            }
            //绘制下半部分
            for (int i = 1; i <= high - 1; i++){
                for (int j = 1; j <= i; j++){
                    System.out.print(' ');
                }
                for (int k = 1; k <= 2 * (high - i) - 1; k++){
                    System.out.print('*');

                }
                System.out.println();
            }
        }
    }



8./*打印出如下图形:    行数            空格              字母
        A                 1          high-1             1
       ABA               2          high-2             3
      ABCBA             3         high-3             5
     ABCDCBA
    ABCDEDCBA
     ABCDCBA
      ABCBA
       ABA
        A
  */
    import java.util.Scanner;
    class demo{
        public static void main(String args[]){
            int high;
            Scanner sc = new Scanner(System.in);
            System.out.println("你想要几层圣诞树？");
            high = sc.nextInt();
            char start = 'A';
            //程序开始
            //绘制上半部分

            //外层循环控制总层数
            for ( int line = 1; line <= high; line++){
                //绘制空格，空格数 = 总高度high - 行数line
                for (int j = 1; j <= high - line; j++ ){
                    System.out.print(" ");
                }
                //绘制左边三角，三角数 = line - 1
                for (int k = 1; k <= line - 1; k++){
                    System.out.print(start);
                    start++;
                }
                //绘制中间列，为行数代表的字符
                System.out.print(start);
                //绘制右边三角形
                start--;
                for (int i = 1; i <= line -1; i++){
                    System.out.print(start);
                    start--;
                }
                //打印回车
                System.out.println();
                 start = 'A';      
            }
            //打印下半部分
            int numberOfChar = high - 2;
            start = 'A';
            for ( int line = 1; line <= high -1; line++){
                //打印空格 空格数 = 行数line；
                for ( int i = 1; i <= line; i++){
                     System.out.print(" ");
                }
                //打印左半三角

                for( int j = 1; j <= numberOfChar; j++){
                    System.out.print(start);
                    start++;

                }
                //打印中间列
                System.out.print(start);
                //打印右半三角
                start--;
                for (int k = 1; k <= numberOfChar; k++){
                    System.out.print(start);
                    start--;
                }
                System.out.println();
                start = 'A';
                numberOfChar--;    
            }
        }
    }
    //过于繁琐，应尽量减少变量数量，增加可读性，能用一个变量解决就不要用两个
    import java.util.Scanner;
      class demo{
        public static void main(String[] args){
            int high;     
            Scanner sc = new Scanner(System.in);
            System.out.println("你想要多高的圣诞树？");
            high = sc.nextInt();
            char start = 'A';
            //程序开始
            for (int i = 1; i <= high; i++){
                //空格数等于 high - 1
                for (int j = 1; j <= high -i; j++){
                    System.out.print(' ');
                }
                //星星数等于 行数 * 2 - 1
                for (int k = 1; k <= i; k++){
                    System.out.print(start++);  
                  }
                start--；         //减去最后一次自增时多出来的一次
                for (int k = 1; k <= high - i - 1; k++){
                    for (int a = 1; a <= i - 1; a++){
                        System.out.print(--start);
                }
                System.out.println();
                start = 'A';
            }
            //绘制下半部分
            for (int i = 1; i <= high - 1; i++){
                for (int j = 1; j <= i; j++){
                    System.out.print(' ');
                }
                for (int k = 1; k <= high - i; k++){
                    System.out.print(start++);     
                }
                start--;         //减去最后一次自增时多出来的一次
                for (int k = 1; k <= high - i - 1; k++){
                    System.out.print(--start);     
                }
                System.out.println();
                start = 'A';
            }
        }
    }
      //舍弃start 使用代码块本身变量控制字符输出，使用类型转换

    import java.util.Scanner;
      class demo{
        public static void main(String[] args){
            int high;     
            Scanner sc = new Scanner(System.in);
            System.out.println("你想要多高的圣诞树？");
            high = sc.nextInt();
            //程序开始
            for (int i = 1; i <= high; i++){
                //空格数等于 high - 1
                for (int j = 1; j <= high -i; j++){
                    System.out.print(' ');
                }

                for (int k = 1; k <= i; k++){
                    char c = 'A';
                    System.out.print((char)(c + k - 1));
                  }

                for (int a = 1; a <= i - 1; a++){
                    char c = 'A';
                    System.out.print((char)(c + i - 1 - a));
                }
                System.out.println();
            }
            //绘制下半部分
            for (int i = 1; i <= high - 1; i++){
                for (int j = 1; j <= i; j++){
                    System.out.print(' ');
                }
                for (int k = 1; k <= high - i; k++){
                    char c = 'A';
                    System.out.print((char)(c + k - 1));     
                }

                for (int k = 1; k <= high - i - 1; k++){
                    char c = 'A';
                    System.out.print((char)(c + high - 2 - k));     
                }
                System.out.println();    
            }
        }
       }                                
9\. /*打印如下图形     7x7          行数           #1    #2     #3      *1
           ###*###                 1             3      0      3       
           ##*#*##                 2             2      1      2       
           #*###*#                 3             1      3      1
           *#####*                 4             0      5      0
           #*###*#                 1                    3
           ##*#*##                 2                    1
           ###*###
    */
    import java.util.Scanner;
    class demo{
        public static void main(String[] args){
            //读取输入的高度和宽度，均为偶数
            Scanner sc_high = new Scanner(System.in);
            System.out.println("请输入想要的高度：");
            int high = sc_high.nextInt();  
            while ( high % 2 != 1){
                System.out.println("输入有误，请重新输入：");
                System.out.println("请输入想要的高度：");
                high = sc_high.nextInt();             
            }
            Scanner sc_width = new Scanner(System.in);
             System.out.println("请输入想要的宽度：");
            int width = sc_width.nextInt();  
            while ( high % 2 != 1){
                System.out.println("输入有误，请重新输入：");
                System.out.println("请输入想要的宽度：");
                width = sc_width.nextInt();             
            }

            //开始绘图
            //打印上半部分
            int numberOfSign = (width - 1)/2;
             //外层循环控制总层数
            for (int line = 1; line <= (high -1)/2; line++){
                //打印#1，#1数量 = (width - 1)/2 ，最终为0

                for (int i = 1;    i <= numberOfSign; i++){
                    System.out.print("#");
                }

                //打印*1
                if (line == 1){
                    System.out.print("*");
                } else {
                    //打印第一个*
                    System.out.print("*");
                    //打印#2
                    for (int i = 1; i <= 2*line - 3; i++){
                        System.out.print("#");
                    }
                    //打印第二个*
                    System.out.print("*");

                }
                //打印#3       
                for (int i = 1; i <= numberOfSign; i++){
                    System.out.print("#");
                }
                 numberOfSign--;
                System.out.println();

            }
            //打印中间部分
            System.out.print("*");
            for (int i = 1; i <= width - 2; i++){
                System.out.print("#");
            }
            System.out.print("*");
            System.out.println();
            //打印下半部分
            //打印#1
            numberOfSign = 1;
            for (int line = (high -1)/2; line > 0; line--){
                //打印#1
                for (int i = 1; i <= numberOfSign; i++){
                    System.out.print("#");                  
                }  
                if (line == 1 ){
                    System.out.print("*");
                } else {x
                    //打印第一个*
                    System.out.print("*");
                    //打印#2
                    for (int i = 1; i <= 2*line - 3; i++){
                        System.out.print("#");
                    }
                    //打印第二个*
                    System.out.print("*");

                }
                //打印#3       
                for (int i = 1; i <= numberOfSign; i++){
                    System.out.print("#");
                }
                numberOfSign++;
                System.out.println();
            }

        }
    }
       //简化，先绘制#阵，再用*去替换
       import java.util.Scanner;
    class demo{
        public static void main(String[] args){
            //读取输入的高度和宽度，均为偶数
            Scanner sc_high = new Scanner(System.in);
            System.out.println("请输入想要的高度：");
            int high = sc_high.nextInt();  
            while ( high % 2 != 1){
                System.out.println("输入有误，请重新输入：");
                System.out.println("请输入想要的高度：");
                high = sc_high.nextInt();             
            }
            Scanner sc_width = new Scanner(System.in);
             System.out.println("请输入想要的宽度：");
            int width = sc_width.nextInt();  
            while ( high % 2 != 1){
                System.out.println("输入有误，请重新输入：");
                System.out.println("请输入想要的宽度：");
                width = sc_width.nextInt();             
            }

            //绘制开始
            int middle = (width + 1) / 2 ;
            for (int i = 1; i <= high; i++){
                for (int j = 1; j <= width; j++){
                    if ( i <= (high + 1) / 2){
                        if ((j == middle + (i - 1)) || (j == middle - (i - 1))){
                        System.out.print('*');
                        continue;
                        }
                        System.out.print('#');
                    } else {
                        if ( j == middle + (high - i) || j == middle - (high - i)){
                        System.out.print('*');
                        continue;
                        }
                        System.out.print('#');
                    }  
                }
                System.out.println();
            }
        }
    }
```
**归纳总结：**

1. **for 循环中，i = 0 与 i < target 搭配 ，i = 1 与 i <= target 搭配**
2. **一定要注意，当需要初始化一个循环量时，在循环外进行赋值**
3. **递减循环中 , 应该使计量数 > 0 , 因为0本身也算一个数**
4. **使用自增自减时，一定要注意，最后一次循环时，仍会进行一次自增自减，需要根据具体情况取舍**
