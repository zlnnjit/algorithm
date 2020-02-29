# 面试题09:用两个栈实现队列

## 题目描述

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )



## 示例

示例 1：



```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```




示例 2：

```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```




提示：

```
1 <= values <= 10000
最多会对 appendTail、deleteHead 进行 10000 次调用
```



## Code

```java
class CQueue {
    //顺序栈
    Stack<Integer> s1;
    //暂存栈
    Stack<Integer> s2;
    public CQueue() {
        s1 = new Stack<>();
        s2 = new Stack<>();
    }
    
    public void appendTail(int value) {
        s1.push(value);
    }
    
    public int deleteHead() {
        if(s1.empty()){
            return -1;
        }
        while(!s1.empty()){
            s2.push(s1.pop());
        }
        int val = s2.pop();
        while(!s2.empty()){
            s1.push(s2.pop());
        }
        return val;
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */
```

## 题解

https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/solution/mian-shi-ti-09-yong-liang-ge-zhan-shi-xian-dui-l-3/

https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/solution/mian-shi-ti-09-yong-liang-ge-zhan-shi-xian-dui-l-2/



其他同学解法：

使用java的同学请注意，如果你使用Stack的方式来做这道题，会造成速度较慢； 这个原因的话是因为Stack继承了Vector接口，而Vector底层是AbstractList，是一个数组，那么就要考虑空间扩容的问题了。 可以使用LinkedList来做Stack的容器，因为LinkedList实现了Deque接口，所以Stack能做的事LinkedList都能做，其本身结构是个链表，扩容消耗少。 但是我的意思不是像100%代码那样直接使用一个List当做队列，那确实是快=，但是不符题意。 贴上代码，这样的优化之后，效率提高了40%，超过97%。

```java
class CQueue {
    LinkedList<Integer> stack1;
	LinkedList<Integer> stack2;
	
	public CQueue() {
		stack1 = new LinkedList<>();
		stack2 = new LinkedList<>();
	}

	public void appendTail(int value) {
		stack1.add(value);
	}

	public int deleteHead() {
		if (stack2.isEmpty()) {
			if (stack1.isEmpty()) return -1;
			while (!stack1.isEmpty()) {
				stack2.add(stack1.pop());
			}
			return stack2.pop();
		} else return stack2.pop();
	}
}
```