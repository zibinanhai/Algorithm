
## 题目地址(1. 两数之和)

https://leetcode-cn.com/problems/two-sum/

## 题目描述

```
给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

示例 1：

输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。

提示：

2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
只会存在一个有效答案

进阶：你可以想出一个时间复杂度小于 O(n2) 的算法吗？
```
## 思路
* 用一个Hashmap来存储元素和元素对应的index
* 遍历数组，判断当前元素与target对应的差值是否在map中存在
* 注：会在解的第二个索引处遍历到

## 关键点
* map的key重复的问题：
* 题目指出解只有一个，如果解的其中一个元素在数组中有相同的元素：
1. 3个或3个以上重复，则解不可能只有一个 
2. 2个，则这两个一定是答案的解（否则问题同上），所以不用考虑map的key会重复的问题
3. 不是解中的元素key被覆盖也没关系，用不到

数组的长度用.length 没括号  

## 代码

- 语言：Java

```java

class Solution {
    public int[] twoSum(int[] nums, int target) throws RuntimeException {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; ++i) {
            int diff = target - nums[i];
            if (map.containsKey(diff)) {
                return new int[]{map.get(diff), i};
            }
            map.put(nums[i], i);
        }
        throw new RuntimeException("twoSum no sulution");
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


