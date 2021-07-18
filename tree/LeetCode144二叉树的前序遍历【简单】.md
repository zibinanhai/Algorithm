
## 题目地址(144. 二叉树的前序遍历)

https://leetcode-cn.com/problems/binary-tree-preorder-traversal/

## 题目描述

```
给你二叉树的根节点 root ，返回它节点值的 前序 遍历。

 

示例 1：

输入：root = [1,null,2,3]
输出：[1,2,3]


示例 2：

输入：root = []
输出：[]


示例 3：

输入：root = [1]
输出：[1]


示例 4：

输入：root = [1,2]
输出：[1,2]


示例 5：

输入：root = [1,null,2]
输出：[1,2]


 

提示：

树中节点数目在范围 [0, 100] 内
-100 <= Node.val <= 100

 

进阶：递归算法很简单，你可以通过迭代算法完成吗？
```

## 前置知识

- 

## 公司

- 暂无

## 思路
* 看注释
## 关键点

-  

## 代码

- 语言支持：Java

Java Code:

```java

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    //有两种方法遍历，递归和非递归，主要看非递归
    //非递归模仿了评论区的颜色标记法，这种方法其实就是模拟了函数栈的调用过程
    //fslse是未标记，即第一次进栈， true是标记过的，即第二次进栈
    //这两次相当于函数递归的第一次进入和递归返回的过程，更接近递归的本质
    //这种迭代对于三种遍历顺序的写法相似，只是换一下进栈的顺序

    // 1.递归解法
    // public List<Integer> preorderTraversal(TreeNode root) {
    //     List<Integer> res = new ArrayList<Integer>();
    //     preorder(root, res);
    //     return res;
    // }

    // public void preorder(TreeNode root, List<Integer> res) {
    //     if (root == null) {
    //         return;
    //     }
    //     res.add(root.val);
    //     preorder(root.left, res);
    //     preorder(root.right, res);
    // }

    // 2.非递归解法
    public List<Integer> preorderTraversal(TreeNode root) {
        Deque<MarkNode> stack = new LinkedList<>();
        List<Integer> res = new ArrayList<>();

        MarkNode r = new MarkNode(root, false);
        stack.push(r);
        while (!stack.isEmpty()) {
            //注意，这里markNode每次都是封装过的所以不会为null，可能为Null的是里面的TreeNode
            MarkNode markNode = stack.poll();
            TreeNode cur = markNode.node;
            if (cur == null) {
                continue;
            }
            if (!markNode.isMarked) {
                stack.push(new MarkNode(cur.right, false));
                stack.push(new MarkNode(cur.left, false));
                stack.push(new MarkNode(cur, true));
            } else {
                res.add(cur.val);
            }
        }
        return res;
    }
    class MarkNode {
        TreeNode node;
        boolean isMarked;

        public MarkNode (TreeNode node, boolean isMarked) {
            this.node = node;
            this.isMarked = isMarked;
        }
    }
}

```


**复杂度分析**

令 n 为节点数。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


