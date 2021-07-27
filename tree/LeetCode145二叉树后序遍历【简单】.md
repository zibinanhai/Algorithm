
## 题目地址(145. 二叉树的后序遍历)

https://leetcode-cn.com/problems/binary-tree-postorder-traversal/

## 题目描述

```
给定一个二叉树，返回它的 后序 遍历。

示例:

输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [3,2,1]

进阶: 递归算法很简单，你可以通过迭代算法完成吗？
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

    // 标准后序非递归写法 （有一种投机的写法是把前序遍历的左右换一下，并Collections.reverse)
    public List<Integer> postorderTraversal(TreeNode root) {
        //思路是三步
        //第一步 走左节点一直走到NullNull
        //第二步 没有右节点时，直接加入res， 并root -> null （已经处理完了，直接返回弹上层节点）
        //第三步 有右节点时，分两种情况： 
        //      1. 没走过 -> 再把当前节点压栈，root指向右节点 (先遍历右节点再遍历根)
        //      2. 走过了 -> 直接加入res, 并root -> null 
        Deque<TreeNode> stack = new LinkedList<>();
        List<Integer> res = new ArrayList<>();
        TreeNode pre = null;
        while (root != null || !stack.isEmpty()) {
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
            //到达最左叶子节点
            root = stack.pop();
            //没有右节点 || 走过右节点了
            if (root.right == null || root.right == pre) {
                res.add(root.val);
                //遍历右节点时，pre会指向右节点，再弹上层节点时就会跳过这个if
                pre = root;
                root = null;
            } else {
                // 没走过 压栈，指向右节点
                stack.push(root);
                root = root.right;
            }
        }
        return res;
    }

    // 递归
    // public List<Integer> inorderTraversal(TreeNode root) {
    //     List<Integer> res = new ArrayList<>();
    //     dfs(root, res);
    //     return res;
    // }
    // private void dfs(TreeNode root, List<Integer> res) {
    //     if (root == null) {
    //         return;
    //     }
    //     dfs(root.left, res);
    //     dfs(root.right, res)
    //     res.add(root.val);
    // }

    // 非递归统一写法，效率较低
    // public List<Integer> postorderTraversal(TreeNode root) {
    //     List<Integer> res = new ArrayList<>();
    //     Deque<MarkNode> stack = new LinkedList<>();

    //     MarkNode r = new MarkNode(root, false);
    //     stack.push(r);

    //     while (!stack.isEmpty()) {
    //         MarkNode node = stack.poll();
    //         TreeNode cur = node.node;
    //         if (cur == null) {
    //             continue;
    //         }
    //         if (!node.isMarked) {
    //             //左右中 中右左
    //             stack.push(new MarkNode(cur, true));
    //             stack.push(new MarkNode(cur.right, false));
    //             stack.push(new MarkNode(cur.left, false));
    //         } else {
    //             res.add(cur.val);
    //         }
    //     }
    //     return res;
    // }

    // class MarkNode {
    //     TreeNode node;
    //     boolean isMarked;

    //     public MarkNode(TreeNode node, boolean isMarked) {
    //         this.node = node;
    //         this.isMarked = isMarked;
    //     }
    // }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


