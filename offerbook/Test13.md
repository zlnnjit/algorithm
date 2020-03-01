# 面试题13: 机器人的运动范围

## 题目描述

地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？



## 示例

示例 1：

```
输入：m = 2, n = 3, k = 1
输出：3
```




示例 2：

```
输入：m = 3, n = 1, k = 0
输出：1
```




提示：

```
1 <= n,m <= 100
0 <= k <= 20
```



# Code

DFS+回溯

```java
class Solution {
    public int movingCount(int m, int n, int k) {
        return helper(m, n, 0, 0, k, new boolean[m][n]);
    }


    private int helper(int m, int n, int x, int y, int k, boolean[][] visited) {
        //越界
        if (x < 0 || y < 0 || x == m || y == n) return 0;

        //已经被访问过
        if(visited[x][y]) return 0;

        //计算位数之和
        int sum = bitSum(x) + bitSum(y);

        //大于k
        if (sum > k) return 0;

        //满足条件
        visited[x][y] = true;


        //深度遍历
        return helper(m, n, x - 1, y, k, visited) +
                helper(m, n, x + 1, y, k, visited) +
                helper(m, n, x, y - 1, k, visited) +
                helper(m, n, x, y + 1, k, visited) + 1;


    }

    //计算位数之和
    private int bitSum(int a) {
        int sum = 0;
        while (a != 0) {
            sum = sum + a % 10;
            a /= 10;
        }
        return sum;
    }
}
```

# 题解

https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/solution/mian-shi-ti-13-ji-qi-ren-de-yun-dong-fan-wei-dfs-b/

