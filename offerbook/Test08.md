# 面试题58：二叉树的下一个结点

题目：给定一颗二叉树和其中的一个结点，如何找出中序遍历的下一个结点？树中的结点除了有两个分别指向左右子结点的指针以外，还有一个指向父结点的指针。

根据题目要求，我们先来定义二叉树的数据结构:

```java
public class TreeLinkNode {
    int val;
    TreeLinkNode left = null;
    TreeLinkNode right = null;
    TreeLinkNode next = null;

    TreeLinkNode(int val) {
        this.val = val;
    }
}
```

思路：如果一个结点有右子树，那么它的下一个结点就是它的右子树中的左子结点。也就是说右子结点出发一直沿着指向左子结点的指针，我们就能找到它的下一个结点。

接着我们分析一个结点没有右子树的情形。如果结点是它父节点的左子结点，那么它的下一个结点就是它的父结点。

如果一个结点既没有右子树，并且它还是它父结点的右子结点，这种情形就比较复杂。我们可以沿着指向父节点的指针一直向上遍历，直到找到一个是它父结点的左子结点的结点。如果这样的结点存在，那么这个结点的父结点就是我们要找的下一个结点。

实现代码：

```java
public TreeLinkNode GetNext(TreeLinkNode pNode) {
    //如果二叉树为空，那么肯定没有下一个结点
    if (pNode == null) {
        return null;
    }
    //如果二叉树有右子树
    if (pNode.right != null) {
        pNode = pNode.right;
        while (pNode.left != null) {
            pNode = pNode.left;
        }
        return pNode;
    }

    //如果二叉树没有右子树
    while (pNode.next != null) {
        //找第一个当前节点是父节点左孩子的节点
        if (pNode.next.left == pNode) {
            return pNode.next;
        }
        pNode = pNode.next;
    }
    return null;

}
```

