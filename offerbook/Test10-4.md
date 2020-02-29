# 面试题10-4: 变态跳台阶

## 题目描述

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。



# Code

```java
public int JumpFloorII(int target) {
    return (int) Math.pow(2, target - 1);
}
```



# 题解

https://github.com/CyC2018/CS-Notes/blob/master/notes/10.4%20%E5%8F%98%E6%80%81%E8%B7%B3%E5%8F%B0%E9%98%B6.md