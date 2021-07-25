
## 题目地址(110. 平衡二叉树)

https://leetcode-cn.com/problems/balanced-binary-tree/

## 题目描述

```
给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1 。

 

示例 1：

输入：root = [3,9,20,null,null,15,7]
输出：true


示例 2：

输入：root = [1,2,2,3,3,null,null,4,4]
输出：false


示例 3：

输入：root = []
输出：true


 

提示：

树中的节点数在范围 [0, 5000] 内
-104 <= Node.val <= 104
```

## 前置知识

- 

## 公司

- 暂无

## 思路

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
    //剪枝 时间复杂度O(N) 自底向上 遍历一次
    public boolean isBalanced(TreeNode root) {
        //定义每个节点应该返回的值，如果子树不是平衡二叉树，直接返回-1
        return dfs(root) != -1; 
    }

    private int dfs(TreeNode root) {
        if (root == null) {
            return 0;
        }
        //把左右子树的判断分开，这样左子树如果不是平衡的，就不用去遍历右子树
        int left = dfs(root.left);
        if (left == -1) {
            return -1;
        }
        int right = dfs(root.right);
        if (right == -1) {
            return -1;
        }
        if (Math.abs(left - right) >= 2) {
            return -1;
        }
        return 1 + Math.max(left, right);
    }

    //不剪枝的方法，复杂度低 O(N2) 自顶向下，每个子树都要遍历一遍
    // public boolean isBalanced(TreeNode root) {
    //     if (root == null) {
    //         return true;
    //     }
    //     return Math.abs(getTreeHeight(root.left) - getTreeHeight(root.right)) <= 1 
    //         && isBalanced(root.left) && isBalanced(root.right);
    // }

    // private int getTreeHeight(TreeNode root) {
    //     if (root == null) {
    //         return 0;
    //     }
    //     return 1 + Math.max(getTreeHeight(root.left), getTreeHeight(root.right));
    // }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


