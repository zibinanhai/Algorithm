
## 题目地址(160. 相交链表)

https://leetcode-cn.com/problems/intersection-of-two-linked-lists/

## 题目描述

```
编写一个程序，找到两个单链表相交的起始节点。


## 公司

- 暂无

## 思路
两个链表如果相交，那从相交到结尾的路程一定是相同的，但是单向链表不能从结尾开始遍历，所以
a + b = b + a
每个链表遍历到链表尾部的时候，去遍历另一个链表，这样就可以保证两个链表是同时到达对方的尾部
如果相交，就一定会在中间同时遍历到
## 关键点

- 
循环的中止条件为headA != headB
内部可以用三元表达式来同步遍历，如果没有相交，最后两个链表都会遍历到Null,退出循环

## 代码

- 语言支持：Java

Java Code:

```java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }
        ListNode tmpA = headA;
        ListNode tmpB = headB;
        while(headA != headB) {
            headA = headA == null ? tmpB : headA.next;
            headB = headB == null ? tmpA : headB.next;
        }
        return headA;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$


