
## 题目地址(199. 二叉树的右视图)

https://leetcode-cn.com/problems/binary-tree-right-side-view/

## 题目描述

```
给定一个二叉树的 根节点 root，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。

 

示例 1:

输入: [1,2,3,null,5,null,4]
输出: [1,3,4]


示例 2:

输入: [1,null,3]
输出: [1,3]


示例 3:

输入: []
输出: []


 

提示:

二叉树的节点个数的范围是 [0,100]
-100 <= Node.val <= 100 
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
    public List<Integer> rightSideView(TreeNode root) {
        //思路，层序遍历取最后一个
        //本题不能直接用一个栈去做，用栈可以保证第二层取的是右视图
        //但是由于第二层是从右到左进栈，第三层的顺序就反了
        //可以用一个双端队列，入队正常入队，每层遍历完了以后取最后一个值即可

        //还有一种思路是dfs,按根-右-左的顺序遍历，每层最先遍历的就是最右边的节点
        //每走一次dfs, d
        if (root == null) {
            return  Collections.emptyList();
        }
        List<Integer> res = new ArrayList<>();
        Deque<TreeNode> q = new LinkedList();
        q.offer(root);
        while (!q.isEmpty()) {
            res.add(q.peekLast().val);
            int length = q.size();
            for (int i = 0; i < length; ++i) {
                TreeNode node = q.poll();
                if (node.left != null) {
                    q.offer(node.left);
                }
                if (node.right != null) {
                    q.offer(node.right);
                }
            } 
        }
        return res;
    }

//     class Solution {
//     List<Integer> res = new ArrayList<>();

//     public List<Integer> rightSideView(TreeNode root) {
//         dfs(root, 0); // 从根节点开始访问，根节点深度是0
//         return res;
//     }

//     private void dfs(TreeNode root, int depth) {
//         if (root == null) {
//             return;
//         }
//         // 先访问 当前节点，再递归地访问 右子树 和 左子树。
//         if (depth == res.size()) {   // 如果当前节点所在深度还没有出现在res里，说明在该深度下当前节点是第一个被访问的节点，因此将当前节点加入res中。
//             res.add(root.val);
//         }
//         //这个深度，在递归返回的时候变成当前层的深度，不会一直累加
//         depth++;
//         dfs(root.right, depth);
//         dfs(root.left, depth);
//     }

}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


