# 数组中移除目标值

在一个给定的数组中，移除所有给定的目标值

## 1. 自己写的版本

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0;
        for (int j = 0; j < nums.length; j++) {
            if (nums[j] != val) {
                nums[i] = nums[j];
                i++;
            }
        } 
        return i;   
        }
}
```

## 2. 如果目标值很稀疏

我们注意到，其实答案并没有要求新数列的顺序与原数列相同；
因此，当目标值很稀疏时，我们可以遍历数组，当遇到目标值时，用最后一个数代替目标值。

```java
class Solution{
    public int removeElement(int[] nums, int val) {
    int i = 0;
    int n = nums.length;
    while (i < n) {
        if (nums[i] == val) {
            nums[i] = nums[n - 1];
            // reduce array size by one
            n--;
        } else {       //因为不能确认数列末尾值是否为目标值，因此移动一次之后还要判断一次移动后的值是否为目标值
            i++;
        }
    }
    return n;
}
}


```

