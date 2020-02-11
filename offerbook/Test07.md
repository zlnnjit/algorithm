## 面试题7：重建二叉树


题目：输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如：前序遍历序列｛ 1, 2, 4, 7, 3, 5, 6, 8｝和中序遍历序列｛4, 7, 2, 1, 5, 3, 8，6}，重建出下图所示的二叉树并输出它的头结点。


首先我们需要构建二叉树的数据结构：
```java
public class TreeNode {
      int val;
      TreeNode left;
      TreeNode right;
      TreeNode(int x) { val = x; }
}

```


实现代码：
```java
public class Test07 {

    /**
     *输入某二叉树的前序遍历和中序遍历的结果，请重建出该二节树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。
     * @param pre 前序遍历
     * @param in 中序遍历
     * @return 树的根节点
     */
    public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
        if (pre==null||in==null||pre.length!=in.length||in.length<1){
            return null;
        }
        return construct(pre,0,pre.length-1,in,0,in.length-1);
    }

    /**
     * @param pre 前序遍历
     * @param ps  前序遍历的开始位置
     * @param pe  前序遍历的结束位置
     * @param in  中序遍历
     * @param is  中序遍历的开始位置
     * @param ie  中序遍历的结束位置
     * @return    树的根结点
     */
    public TreeNode construct(int[] pre, int ps,int pe,int[] in, int is,int ie ){


        //// 开始位置大于结束位置说明已经没有需要处理的元素了(递归出去的条件)
        if (ps > pe) {
            return null;
        }

        // 取前序遍历的第一个数字，就是当前的根结点
        int value = pre[ps];
        int index = 0;

        // 在中序遍历的数组中找根结点的位置
        while (index<=ie&&in[index]!=value){
            index++;
        }

        // 如果在整个中序遍历的数组中没有找到，说明输入的参数是不合法的，抛出异常
        if (index > ie) {
            throw new RuntimeException("输入错误");
        }

        // 创建当前的根结点，并且为结点赋值
        TreeNode treeNode = new TreeNode(value);

        // 递归构建当前根结点的左子树，左子树的元素个数：index-is+1个
        // 左子树对应的前序遍历的位置在[ps+1, ps+index-is]
        // 左子树对应的中序遍历的位置在[is, index-1]      
        treeNode.left = construct(pre, ps + 1, ps + index - is, in, is, index - 1);

        // 递归构建当前根结点的右子树，右子树的元素个数：ie-index个  
        // 右子树对应的前序遍历的位置在[ps+index-is+1, pe]  
        // 右子树对应的中序遍历的位置在[index+1, ie] 
        treeNode.right = construct(pre, ps + index - is + 1, pe, in, index + 1, ie);
        
        //返回创建的根节点
        return treeNode;
    }
}

```



下面对方法进行测试：
我们将二叉树进行中序遍历输出:
```java
// 中序遍历二叉树
public void printTree(TreeNode root) {
    if (root != null) {
        printTree(root.left);
        System.out.print(root.val + " ");
        printTree(root.right);
    }

}

// 普通二叉树
//              1
//           /     \
//          2       3
//         /       / \
//        4       5   6
//         \         /
//          7       8
private void test1() {
    int[] preorder = {1, 2, 4, 7, 3, 5, 6, 8};
    int[] inorder = {4, 7, 2, 1, 5, 3, 8, 6};
    TreeNode root = reConstructBinaryTree(preorder, inorder);
    printTree(root);
}

// 所有结点都没有右子结点
//            1
//           /
//          2
//         /
//        3
//       /
//      4
//     /
//    5
private void test2() {
    int[] preorder = {1, 2, 3, 4, 5};
    int[] inorder = {5, 4, 3, 2, 1};
    TreeNode root = reConstructBinaryTree(preorder, inorder);
    printTree(root);
}

// 所有结点都没有左子结点
//            1
//             \
//              2
//               \
//                3
//                 \
//                  4
//                   \
//                    5
private void test3() {
    int[] preorder = {1, 2, 3, 4, 5};
    int[] inorder = {1, 2, 3, 4, 5};
    TreeNode root = reConstructBinaryTree(preorder, inorder);
    printTree(root);
}

// 树中只有一个结点
private void test4() {
    int[] preorder = {1};
    int[] inorder = {1};
    TreeNode root = reConstructBinaryTree(preorder, inorder);
    printTree(root);
}

// 完全二叉树
//              1
//           /     \
//          2       3
//         / \     / \
//        4   5   6   7
private  void test5() {
    int[] preorder = {1, 2, 4, 5, 3, 6, 7};
    int[] inorder = {4, 2, 5, 1, 6, 3, 7};
    TreeNode root = reConstructBinaryTree(preorder, inorder);
    printTree(root);
}

// 输入空指针
private  void test6() {
    reConstructBinaryTree(null, null);
}

// 输入的两个序列不匹配
private  void test7() {
    int[] preorder = {1, 2, 4, 5, 3, 6, 7};
    int[] inorder = {4, 2, 8, 1, 6, 3, 7};
    TreeNode root = reConstructBinaryTree(preorder, inorder);
    printTree(root);
}


public static void main(String[] args) {
    Test06 t = new Test06();
    t.test1();
    System.out.println();
    t.test2();
    System.out.println();
    t.test3();
    System.out.println();
    t.test4();
    System.out.println();
    t.test5();
    System.out.println();
    t.test6();
    System.out.println();
    t.test7();
}

```

result:
```
4 7 2 1 5 3 8 6 
5 4 3 2 1 
1 2 3 4 5 
1 
4 2 5 1 6 3 7 

Exception in thread "main" java.lang.RuntimeException: 输入错误
.......

```