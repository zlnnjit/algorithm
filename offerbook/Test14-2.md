# 面试题14-1: 剪绳子

## 题目描述

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m] 。请问 k[0]*k[1]*...*k[m] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

**答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。（与上一题区别之处）**

## 示例

示例 1：



```
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```




示例 2：

```
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```




提示：

```
2 <= n <= 1000
```



# Code

```java
class Solution {
    public int cuttingRope(int n) {

        //当 n <= 3 时，按照贪心规则应直接保留原数字，但由于题目要求必须拆分，因此必须拆出一个 1，即直接返回 n - 1；
        if (n <= 3) return n - 1;
        long result = 0;
        //求 n 除以 3 的整数部分 a 和余数部分 b；
        int a = n / 3, b = n % 3;
        //当 b == 0时，直接返回 3^a
        if (b == 0) result = pow(a);
        //当 b == 1 时，要将一个 1 + 3转换为 2+2，此时返回 3^{a-1} * 2 * 2
        if (b == 1) result = (pow(a - 1) * 2 % 1000000007) * 2;
        //当 b == 2 时，返回 3^a * b
        if (b == 2) result = (pow(a) * b);
        return (int) result % 1000000007;
    }

    private int pow(int a){
        long result = 1;
        for (int i = 0; i < a; i++) {
            result = (result * 3) % 1000000007;
        }
        return (int) result;
    }
}
```

# 题解

https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/solution/mian-shi-ti-14-ii-jian-sheng-zi-iitan-xin-er-fen-f/

