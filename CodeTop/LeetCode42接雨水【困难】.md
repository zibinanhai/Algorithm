
## 题目地址(42. 接雨水)

https://leetcode-cn.com/problems/trapping-rain-water/

## 题目描述

```
给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

 

示例 1：

输入：height = [0,1,0,2,1,0,1,3,2,1,2,1]
输出：6
解释：上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 


示例 2：

输入：height = [4,2,0,3,2,5]
输出：9


 

提示：

n == height.length
0 <= n <= 3 * 104
0 <= height[i] <= 105
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

class Solution {
    //这道题思路
    //首先 对于i列，怎么才能知道这一列的雨水量是多少呢？
    //是min(lMax, rMax) - height[i]
    //即i列的雨水量是由左右最高的两列中较小的列决定的

    //所以此题有三种一步一步优化的解法
    //暴力求最大列 -> 备忘录 -> 双指针动态求

    //暴力求 O(N2) O(N)
    //遍历height数组，遍历到i时，算i的蓄水量，找到i左边和右边最大的两列,
    //然后求min(lMax, rMax) - height[i]

    //备忘录 O(N) O(N)
    //先从左右遍历一遍，用两个数组lMax[], rMax[]来存每个节点左右最大的值
    //然后遍历height取每一个i的蓄水量

    //双指针 O(N) O(1)
    //双指针比较巧妙，可以动态地求左右的最大值
    //先用left和right两个指针从左右开始遍历
    //lMax和rMax指向的不再是i列左右的最大值，而是(0...left)和 (right...size-1)的最大值
    //因为i列的需水量是由左右最大值中较小的那个决定的
    //所以对于left，此时知道左边的最大值，对于right，此时知道右边的最大值
    //对比lMax和rMax，如果lMax小，则不管右边最大的是谁，left的蓄水量已经由lMax决定了
    //如果rMax小，则不管左边最大的是谁，right的蓄水量已经由rMax决定了
    
    //简化后核心就四行代码
    //while (left <= right) {
    //     更新lMax
    //     更新rMax
    //     根据lMax和rMax的大小更新res并left++或者right++
    // }
    
    public int trap(int[] height) {
        if (height == null || height.length < 2) {
            return 0;
        }
        int left = 0;
        int right = height.length - 1;
        int lMax = 0;
        int rMax = 0;
        int res = 0;
        while (left <= right) {
            lMax = Math.max(lMax, height[left]);
            rMax = Math.max(rMax, height[right]);
            res += lMax <= rMax ? lMax - height[left++] : rMax - height[right--];
            // 简化一下代码
            // if (lMax <= rMax) {
            //     //找到小的那边就决定了蓄水量
            //     res += lMax - height[left++];
            // } else {
            //     res += rMax - height[right--];
            // }
        }
        return res;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$


