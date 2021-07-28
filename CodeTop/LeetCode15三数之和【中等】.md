
## 题目地址(3sum/">15. 三数之和)

https://leetcode-cn.com/problems/3sum/

## 题目描述

```
给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有和为 0 且不重复的三元组。

注意：答案中不可以包含重复的三元组。

 

示例 1：

输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]


示例 2：

输入：nums = []
输出：[]


示例 3：

输入：nums = [0]
输出：[]


 

提示：

0 <= nums.length <= 3000
-105 <= nums[i] <= 105
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
    //思路  
    //首先对数组进行排序，然后遍历地固定一个nums[i],再用双指针从前后遍历，看相加是否为0
    //关键点
    //一个剪枝，三个去重
    //一个剪枝 -> 当nums[i] > 0 时，后面就不用遍历了直接返回，因为数组排好序，后面和不可能为0
    //固定节点去重 -> 如果nums[i] == nums[i - 1] 可以直接跳过
    //双指针去重 -> 如果nums[left] == nums[left - 1] left往后移
    //            如果nums[right] == nums[right + 1] left往左移
    public List<List<Integer>> threeSum(int[] nums) {
        int len = nums.length;
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null || len < 3) {
            return res;
        }
        Arrays.sort(nums);
        for (int i = 0; i < len; ++i) {
            //剪枝
            if (nums[i] > 0) {
                break;
            }
            //去重
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int left = i + 1;
            int right = len - 1;
            while (left < right) {
                int num = nums[i] + nums[left] + nums[right];
                if (num == 0) {
                    res.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    //找到解的时候去重,并各自走一步继续找解
                    while (left < right && nums[left] == nums[left + 1]) left++;
                    while (left < right && nums[right] == nums[right - 1]) right--;
                    //因为left和right已经是解且跳过重复，所以这里单独走其中一个肯定不能找到解
                    left++;
                    right--;
                }
                if (num < 0) left++;
                if (num > 0) right--;
            }
        }
        return res;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


