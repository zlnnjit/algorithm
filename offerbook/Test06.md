## 面试题6：从尾到头打印链表



题目：输入个链表的头结点，从尾到头反过来打印出每个结点的值.


首先，先建立链表的数据结构：
```java
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }

    ListNode() {

    }
}
```

**解法一：不改变链表结构，使用栈。**
```java
import java.util.ArrayList;
import java.util.Stack;

public class Test05 {
    public static ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
            ArrayList<Integer> list = new ArrayList<>();
            Stack<Integer> stack = new Stack<>();
            while (listNode!=null){
                stack.push(listNode.val);
                listNode = listNode.next;
            }
            while (!stack.isEmpty()){
                list.add(stack.pop());
            }
            return list;
    }

    public static void main(String[] args) {

        ListNode root = new ListNode();
        root.val = 1;
        root.next = new ListNode();
        root.next.val = 2;
        root.next.next = new ListNode();
        root.next.next.val = 3;
        root.next.next.next = new ListNode();
        root.next.next.next.val = 4;
        root.next.next.next.next = new ListNode();
        root.next.next.next.next.val = 5;

        ArrayList<Integer> list = printListFromTailToHead(root);
        System.out.println(list);

    }

}import java.util.ArrayList;
import java.util.Stack;

public class Test06 {
    public static ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
            ArrayList<Integer> list = new ArrayList<>();
            Stack<Integer> stack = new Stack<>();
            while (listNode!=null){
                stack.push(listNode.val);
                listNode = listNode.next;
            }
            while (!stack.isEmpty()){
                list.add(stack.pop());
            }
            return list;
    }

    public static void main(String[] args) {

        ListNode root = new ListNode();
        root.val = 1;
        root.next = new ListNode();
        root.next.val = 2;
        root.next.next = new ListNode();
        root.next.next.val = 3;
        root.next.next.next = new ListNode();
        root.next.next.next.val = 4;
        root.next.next.next.next = new ListNode();
        root.next.next.next.next.val = 5;

        ArrayList<Integer> list = printListFromTailToHead(root);
        System.out.println(list);

    }

}
```

result:
```
[5, 4, 3, 2, 1]
```
**解法二：递归栈**

```java
public class Test051 {
    public static void printListFromTailToHead(ListNode listNode) {
            if (listNode!=null){
                printListFromTailToHead(listNode.next);
                System.out.print(listNode.val+" ");
            }
    }

    public static void main(String[] args) {

        ListNode root = new ListNode();
        root.val = 1;
        root.next = new ListNode();
        root.next.val = 2;
        root.next.next = new ListNode();
        root.next.next.val = 3;
        root.next.next.next = new ListNode();
        root.next.next.next.val = 4;
        root.next.next.next.next = new ListNode();
        root.next.next.next.next.val = 5;

        printListFromTailToHead(root);

    }

}
```

result：
```
5 4 3 2 1
```

**解法三：链表结构，将指针反向，然后从头结点遍历输出。（不推荐）**

指针反向，也衍生出两种解法，递归和非递归

非递归的方式：
```java
 public static ListNode printListFromTailToHead(ListNode head) {
    ListNode prev = null;
    while(head!=null){
        ListNode tmp = head.next;
        head.next = prev;
        prev = head;
        head = tmp;
    }
    return prev;
}

```

递归的方式：
```java
public static ListNode printListFromTailToHead(ListNode head) {
    if (head == null || head.next == null)
        return head;
    ListNode newNode = printListFromTailToHead(head.next);
    head.next.next = head;
    head.next = null;
    return newNode;
}
```

这里递归的方式不是很理解，后面再看看。
    