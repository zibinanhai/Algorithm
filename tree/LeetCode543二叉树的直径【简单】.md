
## 题目地址(543. 二叉树的直径)

https://leetcode-cn.com/problems/diameter-of-binary-tree/

## 题目描述

```
给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过也可能不穿过根结点。

 

示例 :
给定二叉树

          1
         / \
        2   3
       / \     
      4   5    


返回 3, 它的长度是路径 [4,2,1,3] 或者 [5,2,1,3]。

 

注意：两结点之间的路径长度是以它们之间边的数目表示。
```

## 前置知识

- 

## 公司

- 暂无

## 思路
* 简化版的二叉树最大路径和

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
    //这道题就是简化版的最大路径和
    int totalMax = Integer.MIN_VALUE;

    public int diameterOfBinaryTree(TreeNode root) {
        dfs(root);
        return totalMax;
    }
    /**
    函数定义：返回节点给上层节点提供的最大路径长度
    并更新以当前节点为转折点的最大路径长度
     */
    public int dfs(TreeNode root) {
        if (root == null) {
            return 0;
        }
        // 后序遍历
        int left = dfs(root.left);
        int right = dfs(root.right);
        //记录的是边的个数，不用+1
        //也可以像最大路径和一样记录节点个数，最后return的时候-1就行
        totalMax = Math.max(totalMax, left + right);
        return 1 + Math.max(left, right);
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


