
## 题目地址(124. 二叉树中的最大路径和)

https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/

## 题目描述

```
路径 被定义为一条从树中任意节点出发，沿父节点-子节点连接，达到任意节点的序列。同一个节点在一条路径序列中 至多出现一次 。该路径 至少包含一个 节点，且不一定经过根节点。

路径和 是路径中各节点值的总和。

给你一个二叉树的根节点 root ，返回其 最大路径和 。

 

示例 1：

输入：root = [1,2,3]
输出：6
解释：最优路径是 2 -> 1 -> 3 ，路径和为 2 + 1 + 3 = 6

示例 2：

输入：root = [-10,9,20,null,null,15,7]
输出：42
解释：最优路径是 15 -> 20 -> 7 ，路径和为 15 + 20 + 7 = 42


 

提示：

树中节点数目范围是 [1, 3 * 104]
-1000 <= Node.val <= 1000
```

## 前置知识

- 

## 公司

- 暂无

## 思路
* 先确定是什么顺序遍历

## 关键点
* 分清楚子节点返回的三种可能 和 最终最大节点需要左右节点都加起来
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
    //做树的题首先确定是什么顺序遍历
    //这道题需要根据子节点的最大路径和来算父节点的，所以是后续遍历
    //自底向上算每个节点的最大路径和
    //由于路径不能重复，所以每个节点的贡献值只有三种情况
    // 1.本节点 2.本节点加左子节点 3.本节点加右子节点
    int res = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        dfs(root);
        return res;
    }

    /**
    函数定义：计算这个节点的贡献值
     */
    public int dfs(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = Math.max(dfs(root.left), 0);
        int right = Math.max(dfs(root.right), 0);

        //后序遍历
        //计算最大路径和是要把当前节点和左右加上，和给上层提供的值不一样，最大路径和是左右节点都包括
        res = Math.max(res, root.val + left + right);
        //每个节点给上层提供的值 只有三种情况
        return root.val + Math.max(left, right);
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


