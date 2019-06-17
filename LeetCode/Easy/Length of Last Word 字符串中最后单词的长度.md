# 字符串中最后一个单词的长度

给定一个字符串，给出字符串中最后一个单词的长度；<br>
如果没有单词，则返回 0 。

注意事项：
1. 字符串的末尾不一定没有 0 ；
2. 当字符串为空时，注意边界问题。

## 自己写的版本

```java
class Solution {
    public int lengthOfLastWord(String s) {
        if (s == "") return 0;
        int end = s.length() - 1;
        while (end >= 0 && s.charAt(end) == ' ') {
            end--;
        }
        int start = end - 1;
        while (start >= 0 && s.charAt(start) != ' ') {
            start--;
        }
        return end - start;

    }
}
```

## 总结

1. 一个简单的问题，注意“字符串末尾也可能有空格”即可；
2. leetcode 的编译器比 idea 的更为严格，会检查所有的越界问题，即使这种情况根本不会发生；
3. 解决办法就是对敏感的边界处进行严格的限定，考虑极限值；
