
## 题目地址(394. 字符串解码)

https://leetcode-cn.com/problems/decode-string/

## 题目描述

```
给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

 

示例 1：

输入：s = "3[a]2[bc]"
输出："aaabcbc"


示例 2：

输入：s = "3[a2[c]]"
输出："accaccacc"


示例 3：

输入：s = "2[abc]3[cd]ef"
输出："abcabccdcdcdef"


示例 4：

输入：s = "abc3[cd]xyz"
输出："abccdcdcdxyz"

```

## 前置知识

- 

## 公司

- 暂无

## 思路
用一个栈来解决

## 关键点
while循环把[]里面的字符串读出来
-  

## 代码

- 语言支持：Java

Java Code:

```java

class Solution {
    public String decodeString(String s) {
        int len = s.length();
        if(len <= 0) {
            return "";
        }
        Stack<String> stack = new Stack<>();
        for(int i=0; i<len; i++){
            char mid=s.charAt(i);
            if(mid==']'){
                StringBuilder tmp = new StringBuilder();
                while(!stack.peek().equals("[")){
                    tmp.insert(0,stack.pop());
                }
                stack.pop();
                StringBuilder num=new StringBuilder();
                while(!stack.isEmpty() && (stack.peek().charAt(0) >= '0' 
                && stack.peek().charAt(0)<='9')){
                    num.insert(0,stack.pop());
                }
                int number=Integer.parseInt(num.toString());
                StringBuilder sb = new StringBuilder();
                for(int j = 0; j < number; j++){
                    sb.append(tmp);
                }
                stack.push(sb.toString());
            }else{
                StringBuilder sb = new StringBuilder();
                sb.insert(0,mid);
                stack.push(sb.toString());
            }
        }
        StringBuilder res = new StringBuilder();
        while(!stack.isEmpty()){
            res.insert(0,stack.pop());
        }
        return res.toString();
    }
}


```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：O(n)
- 空间复杂度：O(n)

