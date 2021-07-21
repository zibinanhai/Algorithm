
## 题目地址(103. 二叉树的锯齿形层序遍历)

https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/

## 题目描述

```
给定一个二叉树，返回其节点值的锯齿形层序遍历。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

例如：
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7


返回锯齿形层序遍历如下：

[
  [3],
  [20,9],
  [15,7]
]

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
    //刚开始用一个List和一个栈，后来发现用一个双端队列，奇数行addLast(队列)，偶数行addFirst(栈)即可
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        if (root == null) {
            return Collections.emptyList();
        }
        Queue<TreeNode> q = new LinkedList<>();
        List<List<Integer>> res = new ArrayList<>();
        int curLevel = 0;
        q.offer(root);

        while (!q.isEmpty()) {
            Deque<Integer> level = new LinkedList();
            curLevel++;
            int length = q.size();
            for (int i = 0; i < length; ++i) {
                TreeNode node = q.poll();
                if (curLevel % 2 == 0) {
                    // stack.push(node.val);
                    level.addFirst(node.val);
                } else {
                    level.addLast(node.val);
                }
                if (node.left != null) {
                    q.offer(node.left);
                }
                if (node.right != null) {
                    q.offer(node.right);
                }
            }
            res.add(new ArrayList(level));
        }
        return res;
    }
}

```


**复杂度分析**

令 n 为节点数

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


