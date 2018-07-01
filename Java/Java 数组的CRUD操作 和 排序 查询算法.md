### 数组的CRUD操作 和 排序 查询算法

CRUD: Create Read Update Delete

#### Read 查询:

```java
class demo {
    public static void main(String[] args){
        int [] arr = new int[] {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

        int index = indexOf(arr, 6);
        if (index != -1) {
            System.out.println("index = " + index);
        } else {
            System.out.println("Not Found");
        }
    }

    /**
    *在int类型数组array中，找到目标数据find坐在下标
    *@param array 要进行查询操作的int类型数组
    *@param find 要查找的int类型数据
    *@return int类型，返回大于等于0的数据，表示找到了find所在下标；
    *                返回-1，表示运行失败或没有找到
    *                失败原因：1.传入地址为null  2.数组个数为0
    *                          
    */
    public static int indexOf(int[] array, int find){
        //参数合法性判断
        if (null == array || array.length == 0) {
            System.out.println("Error Input");
            return -1;
        }

        //定义一个变量
        int index = -1;

        for (int i = 0; i < array.length; i++){
            if (find == array[i]){
                index = i;
                break;
            }
        }
        return index;

    }
}
```

**例题：**

​ 1\. int[] arr = {1, 2, 4, 5, 6, 7, 8, 9, 10};

​ 静态创建数组。请用代码告诉我元素3的下标是多少?

```java
class demo {
    public static void main(String[] args){
        int[] arr = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

        int index = findIndex(arr);
        if (index != -1) {
            System.out.println("index = " + index);
        } else {
            System.out.println("Not Found");
        }
    }

    /**
    *从指定数组中找出元素值为3的成员下标
    *@param array 要进行查询的int类型数组
    *@return  int 返回元素值为3的下标位置
    *        返回结果大于等于0表示遭到了目标
    *        返回 -1 表示没有找到
    */
    public static int findIndex(int[] array) {
        //参数合法性判断
        //传入数组首地址不能为null，且数组长度不为0
        /*若 array.length == 0 放在 null == array 之前，
        且array引用地址为空，则会报错；
        而遵循短路原则，应把 null == array 放在 array.length == 0 之前
        */
        if (null == array || array.length == 0) {
            System.out.println("传入参数不合法");
            return -1;
        }
        //定义一个变量，用于保存目标数据的下标
        int index = -1;
        for (int i = 0; i < array.length; i++) {
            if (3 == array[i]){
                 index = i;
                break;
            }
        }

        return index;
    }

}
```

​

​ 2\. 用户输入10个数保存到数组中(函数)， 利用函数找出数组中，最大值所在下标

​ (唯一最大值)以及最大值是什么?

```java
import java.util.Scanner;
class demo {
    public static void main(String[] args) {
        int[] array = new int[10];
        getNumberFromKeyboard(array);
        int index = findMaxIndexInArray(array);
        if (index > -1){
            System.out.println("max index at " + index + " is " + array[index]);
        } else {
            System.out.println("Error Input");
        }

    }
    /**
    *从键盘上获取10个int的数据，保存到数组中
    *@param int[] 要保存数据的int类型数据
    */
    public static void getNumberFromKeyboard(int[] arr) {
        if (null == arr || arr.length == 0){
            System.out.println("Error Input");
            return ;
        }

        Scanner sc = new Scanner(System.in);
        for (int i = 0; i < arr.length; i++){
            arr[i] = sc.nextInt();
        }
        return ;
    }

    /**
    *找出数组中的最大值的下标
    *@param int[] 要查询最大值的数组
    *@return 返回大于等于0的数据表示找到的最大值下标
    *        返回-1表示函数运行失败
    *        原因：1.传入地址为null
                 2.传入数组成员数为0
    */
    public static int findMaxIndexInArray(int[] arr) {
        if (null == arr || arr.length == 0){
            System.out.println("Error Input");
            return -1;
        }
        //定义一个变量，用来保存最大值所在下标
        int index = 0;
        //遍历数组，找出最大值
        //数组容量为10，i的最大值为9，这里用 <
        for (int i = 1; i < arr.length; i++ ) {        
            if (arr[index] < arr[i]){
                index = i;
            }
        }

        return index;
    }
}
```

​ 3.找出数组中的最大值，放到数组中下标为0的元素位置。 (选择排序算法推演)，再将第二大的数据放到下标为1的位置

```java
import java.util.Scanner;
class demo {
    public static void main(String[] args) {
        int[] arr = new int[10];
        System.out.println("请输入10个数：");
        getNumberFromKeyboard(arr);

        printIntArray(arr);
        putMaxAtZeroIndex(arr);
        printIntArray(arr);
        System.out.println(arr[0]);

    }
    /*
    找出数组中的最大值，放到下标为0的位置
    */

    /**
    *找出int数组arr中的最大值，放到下标为0的位置
    *@param arr 要处理的数组
    *@return boolean 返回true表示函数运行成功
    *                返回false表示函数运行失败
    *                失败原因：1.传入的数据为null 2.数组的元素个数为0
    */
    public static boolean putMaxAtZeroIndex(int[] arr){
        //参数合法性判断
        if (null == arr || arr.length == 0){
            System.out.println("Error Input");
            return false;
        }

        //1.找出最大值所在下标
        int index = 0;
        for (int i = 1; i < arr.length; i++){
            if (arr[index] < arr[i]){
                index = i;
            }
        }

        //和下标为0的元素交换
        int temp = arr[index];
        arr[index] = arr[0];
        arr[0] = temp;
        return true;
    }

    public static boolean getNubmerFromKeyboard(int[] arr) {
        if (null == arr || arr.length == 0){
            System.out.println("Error Input");
            return false;
        }

        Scanner sc = new Scanner(System.in);
        for (int i = 0; i < arr.length; i++){
            arr[i] = sc.nextInt();
        }
        return true;
    }

    public static boolean printIntArray(int[] arr){
        if (null == arr || arr.length == 0){
            System.out.println("Error Input");
            return false;
        }
        for (int i = 0; i < arr.length; i++){
            System.out.println("arr[" + i + "]" + " = " + arr[i]);
        }

        return true;
    }
}
```

#### 查询：排序算法

```java
class demo {
    public static void main(String[] args){
        System.out.println("Please enter 10 intigers :");
        int[] arr = new int[10];
        getNumberFromKeyboard(arr);
        selectSort(arr);
        printIntArray(arr);
    }

    /**
    *SelectSort 选择排序算法
    *@param arr 要进行需爱选择排序的数组
    *@return boolean 返回ture表示运行成功，false表示失败
    */

    public static boolean selectSort(int[] arr){
        if (null == arr || arr.length == 0){
            System.out.println("Error Input");
            return false;
        }
        //外层循环控制查询次数，比数据总数少1，最后只剩1个数时不需要比较
        for (int i = 0; i < arr.length - 1; i++){
            int index = i;
            //找出最大值
            for (int j = i + 1; j < arr.length; j++){
                if (arr[index] < arr[j]){
                index = j;
                }
            }

            //2.判断，交换位置
            if (index != i) {
                int temp = arr[index];
                arr[index] = arr[i];
                arr[i] = temp;
            }
          }
         return true;  
    }

    public static boolean getNumberFromKeyboard(int[] arr) {
        if (null == arr || arr.length == 0){
            System.out.println("Error Input");
            return false;
        }

        Scanner sc = new Scanner(System.in);
        for (int i = 0; i < arr.length; i++){
            arr[i] = sc.nextInt();
        }
        return true;
    }
    public static boolean printIntArray(int[] arr){
        if (null == arr || arr.length == 0){
            System.out.println("Error Input");
            return false;
        }
        for (int i = 0; i < arr.length; i++){
            System.out.println("arr[" + i + "]" + " = " + arr[i]);
        }

        return true;
    }
}
```

#### 查询：二分法查找

基本要求：
　　在数组中的数据必须是有序的，无论是升序还是降序 
　　数据准备： {12， 34， 56， 78， 90，110，120，911，10000} 
　　查询10000 
第一次： int minIndex = 0; int maxIndex = 9; int midIndex = 4; 
　　90 < 10000 因为这里90小于10000，90左边的数均小于10000 minIndex = midIndex + 1; 
第二次： minIndex = 5； maxIndex = 9； midIndex = 7; 
....... 
第四次： minIndex = 9; maxIndex = 9; midIndex = 9, 10000 == 10000 
总结： 
　　前提条件：数组是一个升序数组 如果中间值大于目标值，maxIndex = midIndex - 1; 
　　如果中间值小于目标值，minIndex = midIndex + 1; 
　　如果没有找到，终止条件是：minIndex > maxIndex;

```java
class demo {
    public static void main(String[] args) {
        int[] arr = new int[] {12， 34， 56， 78， 90，110，120，911，10000};

        int index = halfSearch(arr, 110);
        System.out.println("index  = " + index);
    }
    /**
    *二分法查找，在目标数组中，找到目标数组find
    *@param arr 是一个int类型的升序数组
    *@param find int类型,要查询的目标数组
    *@return int 返回大于等于0，表示找到数据，返回-1，表示没有找到数据
    */
    public static int halfSearch(int[] arr, int find) {
        //参数合法性判断
        if (null == arr || arr.length == 0) {
            System.out.println("Error Input");
            return -1;
        }

        int mid = 0;
        int minIndex = 0;
        int maxIndex = arr.length;

        mid = (maxIndex + minIndex) / 2;
        //终止循环条件:找到了目标数据
        while (arr[mid] != find) {

            if (arr[mid] < find) {
                minIndex = mid + 1;        
            } else if (arr[mid] > find) {
                maxIndex = mid - 1;
            }

            if (maxIndex < minIndex){
                mid = -1;
                break;
            }

            mid = (maxIndex + minIndex) / 2;
        }

        return mid;
    }

}
```

​ **选择排序,不寻找下标算法：**

```java
class demo {
    public static void main(String[] args){
        int[] arr = new int[10];
        getNumberFromKeyboard(arr);
        antiSelectSort(arr);
        printIntArray(arr);
    }

    /**
    *选择排序算法，不寻找下标版本
    *@param arr 需要进行排序的数组
    *@retrun boolean 返回true表示运行成功，返回false表示运行失败
    */
    public static boolean antiSelectSort(int[] arr) {
        if (null == arr || arr.length == 0) {
            System.out.println("Error Input");
            return false;
        }
        for (int i = 0; i < arr.length; i++) {

               for (int j = 1; j < arr.length - i; j++) {
                if (arr[j - 1] < arr[j]) {
                    int temp = arr[j - 1];
                    arr[j - 1] = arr[j];
                    arr[j] = temp;
                   }
            }   
        }
        return true;
    }

    public static boolean getNumberFromKeyboard(int[] arr) {
        if (null == arr || arr.length == 0){
            System.out.println("Error Input");
            return false;
        }
        Scanner sc = new Scanner(System.in);
        for (int i = 0; i < arr.length; i++) {
            arr[i] = sc.nextInt();
        }
        return true;    
    }

    public static boolean printIntArray(int[] arr) {
        if (null == arr || arr.length == 0) {
            System.out.println("Error Input");
            return false;
        }

        for (int i = 0; i < arr.length; i++) {
            System.out.println("arr[" + i + "] = " + arr[i]);
        }
        return true;
    }
}
```

```
4.找出数组中的所有的最大值下标
```

```java
class demo {
    public static void main(String[] args){
        int[] arr = new int[] {1, 2, 3, 4, 5, 6, 7, 7, 8, 9};
        int[] indexes = new int[arr.length];

        int count = findAllIndexesInArray(arr, indexes);
        for (int i = 0; i < count; i++){
            System.out.println("Max is " + arr[indexes[i]] + " at " + indexes[i]);
        }
    }

    /*
    找出数组中的所有的最大值下标
    分析：
        函数的返回值只能返回一个
        用一个数组保存最大值的下标

        返回值：返回找到的最大值的个数
    /**
    *从数组中找出所有的最大值下标，放入index[]数组中，返回找到的最大值个数
    *@param arr int类型数组，查询最大值的数组
    *@param indexes 用于保存最大值所在下标
    @return int 返回找到的最大值个数；若返回-1， 表示运行失败
    */
    public static int findAllMaxIndexesInArray(int[] arr, int[] indexes){
        //合法性判断
        if (null == arr || null == indexes || arr.length == 0 || indexes.length == 0){
            System.out.println("Erroe Input");
        }

        //1.确定最大值是谁
        int max = -1000;
        for (int i = 0; i < arr.length; i++){
            if (max < arr[i]){
                max = arr[i];
            }
        }
        //max为最大值
        //2.利用循环找出所有最大值的下标，保存到indexes数组中
        int count = 0;     //计数，最大值个数
        for (int i = 0; i < arr.length; i++){
            if (max == arr[i]){
                indexes[count++] = i;    //重点步骤
            }
        }
        return count;
    }
}
```

#### Update 修改
随后的项目中会详细讲解

#### Create 增加

​ int[] arr = {1, 3, 5, 7, 9, 11, 13, 15, 17, 0};

​ 要求:

​ 1\. 数组是排序完整的，从小到大排序

​ 2\. 0是无效元素!!!

​ 3\. 增加数据，不能影响原本的数组从小到大的排列顺序1

​ 添加操作:

​ **情况1:**

​ 添加一个 10，放入到原本是11的位置，也就是说在9之后

​ {1, 3, 5, 7, 9, **10**, 11, 13, 15, 17};

​ 10 在index = 5 之后的元素**整体向右**移动 移动了4个数据

​ **情况2:**

​ 添加一个9，放入到原本是11的位置

​ {1, 3, 5, 7, 9, **9**, 11, 13, 15, 17};

​ 9在index = 5，之后的元素**整体向右**移动 移动了4个数据

​ **情况3:**

​ 添加一个20，放入到17之后，数组中没有任何元素大于20

​ {1, 3, 5, 7, 9, 11, 13, 15, 17, **20**};

​ 20在index = 9 ，数组不用移动任何元素

​

​ **添加流程:**

​ 1\. 确定数据放入的位置

​ 找出数组中第一个比要插入数据大的元素，该元素所在下标就是要放入数据的位置

​ 如果没有任何一个元素大于要插入的数据，那么这个数据放入到数组的末尾

​ 2\. 考虑数组的移动问题

​ 移动的方式，是从最后一个元素开始，到目标位置，从后往前挨个向右移动一位

​ 如果该数是放入到数组的末尾，那么不需要移动操作

​ 3\. 把要插入的数据，放入到数组中

**tips:初始化插入元素默认位置为该数组的最大下标**

```java
class demo {
    public static void main(String[] args) {
        int[] arr = new int[] {1, 3, 5, 7, 9, 11, 13, 15, 17, 0};

        insertNumberIntoArray(arr,10);

        printIntArray(arr);
    }
    /**
    *arr是一个已经排序完成的数组，从小到大，要将insert数据在不影响数组排序的情况下，放入到数组中
    *@param arr int类型，从小到大排序的数组
    *@param insert 要插入的int类型数据
    *@return boolean类型，返回true表示运行成功，返回false表示运行失败
    */
    public static boolean insertNumberIntoArray (int[] arr, int insert) {
        if (null == arr || arr.length == 0) {
            System.out.println("Error Input");
            return false;
        }

        //1.确定数组放入的位置
        //1.1 假设在数中没有比insert更大的数据
        int index = arr.length - 1;

        //1.2 利用循环遍历数组，找出数中比insert大的一个数组
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] > insert) {
                index = i;//插入数据要放入的下标位置
                break;
            }
        }
        //2\. 考虑数组的移动问题
        /*
        {1, 3, 5, 7, 9, 11, 13, 15, 17, 0}
        放入： 10 index = 5 ,右移进行4次
        放入： 2  index = 1 ,右移进行8次
        放入： 19 index = 9 ,右移进行0次
        移动时,前一位的值赋给后一位，arr[9] = arr[8] ， arr[8] = arr[7]
        即 arr[i] = arr[i - 1] 或 arr[i + 1] = arr[i]
        */
        for (int i = arr.length - 1; i > index; i--) {
            arr[i] = arr[i -1];
        }

        //3\. 把要插入的数据，放入到数组中
        arr[index] = insert;

       return true;
    }

    public static boolean printIntArray(int[] arr) {
        if (null == arr || arr.length == 0) {
            System.out.println("Error Input");
            return false;
        }

        for (int i = 0; i < arr.length; i++) {
            System.out.println("arr[" + i + "] = " + arr[i]);
        }
        return true;
    }
}
```

#### Delete 删除

​ int[] arr = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};

​ 要求:

​ 1\. 0是无效元素，可以在删除过程中，用于填充空位

​ 2\. 删除操作，不能影响原本数据的排列

​ 删除操作:

​ 情况1:

​ 删除 17 index = 8 之后的元素要**向左移动** 1位

​ {1, 3, 5, 7, 9, 11, 13, 15, 19, 0};

​ 情况2:

​ 删除 11 index = 5 之后的元素要**向左移动** 4位

​ {1, 3, 5, 7, 9, 13, 15, 17, 19, 0};

​ 情况3:

​ 删除19 index = 9 不需要 **向左移动**

​ {1, 3, 5, 7, 9, 11, 13, 15, 17, 0};

​ 情况4:

​ 删除 2 没有该数据，无法删除

​ 删除流程:

​ 1\. 要找到删除数所在下标

​ 存在该数，不存在该数

​ 2\. 删除操作

​ 3\. 最后的数据换成0 占位，表示无效数据

```java
class demo {
    public static void main(String[] args) {
        int[] arr = new int[] {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};
        deleteIntInArray(arr,5);
        printIntArray(arr);
    }

    /*
    1.找到删除数所在的下标
    2.删除
    3.最后的数据换成0占位
    */
    /**
    *删除在已排序的数组arr中的delete数据，有可能无法删除
    *@param arr int类型数组，已经排序
    *@param delete 要进行删除的数组
    *@return boolean 返回true表示运行成功，返回false表示运行失败
    */
    public static boolean deleteIntInArray(int[] arr, int delete) {
        if (null == arr || arr.length == 0) {
            System.out.println("Error Input");
        }
        //1\. 判断是否有需要删除的数据
        //1.1假设该数不存在
        int index = -1;
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == delete) {
                index = i;
                break;
            }
        }
        //2.删除
        if ( index != -1) {
            for (int i = index; i < arr.length - 1; i++) {
                arr[i] = arr[i + 1];
            }
            //3.最后的数据换成0占位
            arr[arr.length - 1] = 0;
            return true;   
        } else {
            System.out.println("Error Input");
            return false;
        }
    }

    public static boolean printIntArray(int[] arr) {
        if (null == arr || arr.length == 0) {
            System.out.println("Error Input");
            return false;
        }

        for (int i = 0; i < arr.length; i++) {
            System.out.println("arr[" + i + "] = " + arr[i]);
        }
        return true;
    }
}
```

#### 数组中常见异常

ArrayIndexOutOfBoundsException: 数组操作下标越界 NullPointerException 空指针异常 操作null地址空间异常
