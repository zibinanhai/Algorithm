
## 题目地址(3. 无重复字符的最长子串)

https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/

## 题目描述

```
给定一个字符串 s ，请你找出其中不含有重复字符的 最长子串 的长度。

 

示例 1:

输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。


示例 2:

输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。


示例 3:

输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。


示例 4:

输入: s = ""
输出: 0


 

提示：

0 <= s.length <= 5 * 104
s 由英文字母、数字、符号和空格组成
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
    //滑动窗口
    //这道题的核心就一句话“没重复end往前走，重复了更新start"
    //维护一个最大值和map，map的key是字符
    //value是字符对应的下一个位置，当这个字符重复时，可以用这个value来更新start（start可能
    //因为其他字符的重复已经越过了这个value值，所以start需要取max(value, start)
    //比如pwwp,到第二个p时，不能直接取第一个p的value,因为w的重复start已经到第二个w的位置
    public int lengthOfLongestSubstring(String s) {
        int res = 0;
        int length = s.length();
        Map<Character, Integer> map = new HashMap<>();
        for (int start = 0, end = 0; end < length; ++end) {
            char cur = s.charAt(end);
            if (map.containsKey(cur)) {
                //重复了，则更新start
                start = Math.max(start, map.get(cur));
            }
            //end每走一步都更新map和res
            res = Math.max(res, end - start + 1);
            map.put(cur, end + 1);
        }
        return res;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


