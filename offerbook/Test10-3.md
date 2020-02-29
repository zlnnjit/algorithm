# 面试题10-3: 矩形覆盖



## 题目描述

我们可以用 2`*`1 的小矩形横着或者竖着去覆盖更大的矩形。请问用 n 个 2`*`1 的小矩形无重叠地覆盖一个 2`*`n 的大矩形，总共有多少种方法？



# Code

```java
public int RectCover(int n) {
    if (n <= 2)
        return n;
    int pre2 = 1, pre1 = 2;
    int result = 0;
    for (int i = 3; i <= n; i++) {
        result = pre2 + pre1;
        pre2 = pre1;
        pre1 = result;
    }
    return result;
}
```

# 题解

https://github.com/CyC2018/CS-Notes/blob/master/notes/10.2%20%E7%9F%A9%E5%BD%A2%E8%A6%86%E7%9B%96.md

