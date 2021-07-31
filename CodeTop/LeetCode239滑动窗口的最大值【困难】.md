
## 题目地址(239. 滑动窗口最大值)

https://leetcode-cn.com/problems/sliding-window-maximum/

## 题目描述

```
给你一个整数数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。

返回滑动窗口中的最大值。

 

示例 1：

输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
输出：[3,3,5,5,6,7]
解释：
滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7


示例 2：

输入：nums = [1], k = 1
输出：[1]


示例 3：

输入：nums = [1,-1], k = 1
输出：[1,-1]


示例 4：

输入：nums = [9,11], k = 2
输出：[11]


示例 5：

输入：nums = [4,-2], k = 2
输出：[4]

 

提示：

1 <= nums.length <= 105
-104 <= nums[i] <= 104
1 <= k <= nums.length
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
    //如果每次窗口移动都去计算一个最大值，则复杂度是O(KN)
    //这道题用单调队列来解
    //维护一个双端队列，大的放在前面，每次移动进行两个操作
    //去尾：单调队列维护的是有可能是区间最大的数，如果 321 后面要加的数字是 5，因为后进来的，最后才出去，所以321永远不可能是区间最大的数，所以后面加5以后，就要删去321
    //去头：每次移动的时候判断队列最左边的是否超过左边界，超过就删去
    public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null) return null;
        //建立队列
        int[] res = new int[nums.length - k + 1];
        Deque<Integer> queue = new LinkedList<>();

        //遍历 
        for (int left = 0, right = 0; right < nums.length; ++right) {
            //去尾  可能有多个
            //注意 要分清，存的是下标，比的时候要用数组中的数
            while (!queue.isEmpty() && nums[right] >= nums[queue.peekLast()]) {
                queue.pollLast();
            }
            //当前节点入队(存的是索引，便于判断左边界)
            queue.offer(right);
            //判断左边界，
            left = right - k + 1;
            //去头
            if (!queue.isEmpty() && queue.peekFirst() < left) {
                queue.pollFirst();
            }
            //窗口形成时加入结果
            if (right + 1 >= k)
                res[left] = (nums[queue.peekFirst()]);
        }
        return res;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


