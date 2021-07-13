
## 题目地址(21. 合并两个有序链表)

https://leetcode-cn.com/problems/merge-two-sorted-lists/

## 题目描述

```
将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

 

示例 1：

输入：l1 = [1,2,4], l2 = [1,3,4]
输出：[1,1,2,3,4,4]


提示：

两个链表的节点数目范围是 [0, 50]
-100 <= Node.val <= 100
l1 和 l2 均按 非递减顺序 排列
```

## 思路

## 关键点

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
    //第一种写法，新建一个链表，遍历与比较l1和l2，其中一个为null的时候，next为另一个
    // public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    //     if (l1 == null && l2 == null) {
    //         return null;
    //     }
    //     ListNode dummy = new ListNode(-1);
    //     ListNode itr = dummy;
    //     while (l1 != null && l2 != null) {
    //         if (l1.val <= l2.val) {
    //             itr.next = new ListNode(l1.val);
    //             l1 = l1.next;
    //         } else {
    //             itr.next = new ListNode(l2.val);
    //             l2 = l2.next;
    //         }
    //         itr = itr.next;
    //     }
    //     itr.next = l1 == null ? l2 : l1;
    //     return dummy.next;
    // }

   //递归写法，相当于每次递归找到一个较小节点
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;

        if (l1.val <= l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            //谁小第一个节点就是谁，最后返回谁
            return l1;
        } else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$


