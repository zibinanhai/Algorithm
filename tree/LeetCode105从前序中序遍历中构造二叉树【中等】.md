
## 题目地址(105. 从前序与中序遍历序列构造二叉树)

https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

## 题目描述

```
给定一棵树的前序遍历 preorder 与中序遍历  inorder。请构造二叉树并返回其根节点。

 

示例 1:

Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]


示例 2:

Input: preorder = [-1], inorder = [-1]
Output: [-1]


 

提示:

1 <= preorder.length <= 3000
inorder.length == preorder.length
-3000 <= preorder[i], inorder[i] <= 3000
preorder 和 inorder 均无重复元素
inorder 均出现在 preorder
preorder 保证为二叉树的前序遍历序列
inorder 保证为二叉树的中序遍历序列
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
    //无重复元素
    //有两种方法，一种是传下标，这种要注意下标处理
    //第二种是Arrays.copyOfRange() 左子树分两个数组，又子树分两个数组
    //关于在中序遍历数组中找root的时候每次都要遍历的问题，可以提前用hashmap来存下来每一个节点对应的索引
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return dfs(preorder, 0, preorder.length - 1, inorder, 0, preorder.length - 1);
    }
    public TreeNode dfs(int[] preorder, int preStart, int preEnd, 
    int[] inorder, int inStart, int inEnd) {
        if (preStart > preEnd || inStart > inEnd) {
            return null;
        }
        int rootVal = preorder[preStart];
        int index = -1;
        for (int i = inStart; i <= inEnd; ++i) {
            if (inorder[i] == rootVal) {
                index = i;
                break;
            }
        }
        TreeNode root = new TreeNode(rootVal);
        int left = index - inStart;
        int right = inEnd - index;
        root.left = dfs(preorder, preStart + 1, preStart + left, 
        inorder, inStart, index - 1);
        root.right = dfs(preorder, preStart + left + 1, preEnd,
        inorder, index + 1, inEnd);
        return root;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


