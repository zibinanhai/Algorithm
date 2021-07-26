
## 题目地址(113. 路径总和 II)

https://leetcode-cn.com/problems/path-sum-ii/

## 题目描述

```
给你二叉树的根节点 root 和一个整数目标和 targetSum ，找出所有 从根节点到叶子节点 路径总和等于给定目标和的路径。

叶子节点 是指没有子节点的节点。

 

示例 1：

输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]


示例 2：

输入：root = [1,2,3], targetSum = 5
输出：[]


示例 3：

输入：root = [1,2], targetSum = 0
输出：[]


 

提示：

树中节点总数在范围 [0, 5000] 内
-1000 <= Node.val <= 1000
-1000 <= targetSum <= 1000
```

## 前置知识

- 

## 公司

- 暂无

## 思路
* list保持着当前走过的路，所以到叶子节点或者递归返回的时候，要把list中当前节点删除（回溯）
* 然后每次找到一条路径的时候，复制一份list添加到全局变量res里面
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
    List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        dfs(root, targetSum, new ArrayList<>());
        return res;
    }

    public void dfs(TreeNode root, int sum, List<Integer> list) {
        if (root == null) {
            return;
        }
        list.add(root.val);
        if (root.left == null && root.right == null) {
            //到达叶子节点
            if (root.val == sum) {
                res.add(new ArrayList(list));
                //这里不用清空list，回溯会删掉当前节点
                //相当于list时刻存的都是当前走的路径
            }
            list.remove(list.size() -  1);
            //到叶子节点就返回
            return;
        }

        dfs(root.left, sum - root.val, list);
        dfs(root.right, sum - root.val, list);
        //左右都走完了，返回上一层要把当前这个节点删掉
        list.remove(list.size() - 1);
    }

}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


