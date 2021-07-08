
## 题目地址(206. 反转链表)

https://leetcode-cn.com/problems/reverse-linked-list/

## 题目描述

```
给你单链表的头节点 head ，请你反转链表，并返回反转后的链表。

 

示例 1：

输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]


提示：

链表中节点的数目范围是 [0, 5000]
-5000 <= Node.val <= 5000

 

进阶：链表可以选用迭代或递归方式完成反转。你能否用两种方法解决这道题？
```

## 思路
* 记住下一个节点的联系方式
* 初始化一个null的pre，然后遍历反转即可

## 关键点
* 最后返回的是pre不是cur
-  

## 代码

- 语言支持：Java

Java Code:

```java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        //不需要判空，空了直接返回初始化的pre,就是Null
        ListNode pre = null;
        //用cur复制一下head，更好理解
        ListNode cur = head;
        while (cur != null) {
            //留下联系方式
            ListNode next = cur.next;
            //反转
            cur.next = pre;
            //前进
            pre = cur;
            cur = next;
        }
        return pre;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$


