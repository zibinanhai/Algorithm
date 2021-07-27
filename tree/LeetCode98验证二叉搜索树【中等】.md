
## 题目地址(98. 验证二叉搜索树)

https://leetcode-cn.com/problems/validate-binary-search-tree/

## 题目描述

```
给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

节点的左子树只包含小于当前节点的数。
节点的右子树只包含大于当前节点的数。
所有左子树和右子树自身必须也是二叉搜索树。

示例 1:

输入:
    2
   / \
  1   3
输出: true


示例 2:

输入:
    5
   / \
  1   4
     / \
    3   6
输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
     根节点的值为 5 ，但是其右子节点值为 4 。

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
    //第一种方法，中序遍历判断是不是升序
    //测试用例有root.val = Integer.MIN_VALUE，所以pre要用Long最小值
    // long pre = Long.MIN_VALUE;
    // public boolean isValidBST(TreeNode root) {
    //     Deque<TreeNode> stack = new LinkedList<>();
    //     while (root != null || !stack.isEmpty()) {
    //         while(root != null) {
    //             stack.push(root);
    //             root = root.left;
    //         }
    //         root = stack.pop();
    //         if (root.val <= pre) {
    //             return false;
    //         }
    //         pre = root.val;
    //         root = root.right;
    //     }
    //     return true;
    // }

    //第二种方法，可以给二叉搜索树每个节点定义一个上下界
    //      5
    //   1     7
    //       4    8
    //          6    9
    //主要要避免的是，不能直接判断每个节点的左节点比自己小并且右节点比自己大，因为比如上图的情况
    //4 < 7 但是并不>5 所以不是二叉搜索树

    // 可以跟着代码画一下，每个节点左子树的上界是自己， 右子树的下界是自己 就可以
    // 到了4这个位置，下界是5，上界是7
    // 到了8这个位置, 下界是7， 上界是初始值
    // 到了6这个位置, 下界是5， 上界是8
    public boolean isValidBST(TreeNode root) {
        return dfs(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public boolean dfs(TreeNode root, long lower, long upper) {
        if (root == null) {
            return true;
        }
        if (root.val <= lower || root.val >= upper) {
            return false;
        }
        return dfs(root.left, lower, root.val) && dfs(root.right, root.val, upper);
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


