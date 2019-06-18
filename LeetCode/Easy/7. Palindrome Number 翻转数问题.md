# 翻转数问题

判断一个数，若将其顺序完全倒转，判断翻转结果是否与倒转前一致。<br>
返回一个 boolean 类型值；<br>
 若输入为负数，则直接判断 false。<br>

## 1. 自己写的版本

```java
class Solution {
    public boolean isPalindrome(int x) {
        if ( x < 0)  return false;
         //计算位数
        int length = 0;
        int temp = x;
        while (temp != 0) {
            temp /= 10;
            length++;
        }
        temp = x;
        int[] array1 = new int[length];
        int[] array2 = new int[length];
        int i = 0;
        int templength = length;
        //正序数列
        while (temp != 0) {
            array1[i] = (int)(temp / Math.pow(10, templength - 1));
            temp = (int)(temp % Math.pow(10, templength - 1));
            i++;
            templength--;
        }
        //倒序数列
        int j = length -1;
        temp = x;
        templength = length;
        while (temp != 0) {
            array2[j] = (int)(temp / Math.pow(10, templength - 1));
            temp = (int)(temp % Math.pow(10, templength - 1));
            j--;
            templength--;
        }
        //比较
        for (i = 0; i < length; i++) {
            if (array1[i] != array2[i]) {
                return false;
            }
        }
        return true;
    }
}
```

## 2. 存在的问题

1. 对于这类，重点在于字符而不在值大小的问题，应将 x 转为字符串求解；
2. 求数列长度可以直接使用 String 类下的 valueof 方法，不需要自我实现；

```java
String str = String.valurof(x);
int end = str.length() - 1;
```

3. 根本不需要创建两个数组来分别存储正序倒序的值，直接在 x 转为字符串的基础上，每一步都进行相应字符位置的比较即可；

## 3. 优良版本

```java
public boolean isPalindrome(int x) {
    String str = String.valueOf(x);
    int start = 0;
    int end = str.length() - 1;
    while(start < end){
        if(str.charAt(start++) != str.charAt(end--)) return false;
    }
    return true;
}
```

