
## 题目地址(92. 反转链表 II)

https://leetcode-cn.com/problems/reverse-linked-list-ii/

## 题目描述

```
给你单链表的头指针 head 和两个整数 left 和 right ，其中 left <= right 。请你反转从位置 left 到位置 right 的链表节点，返回 反转后的链表 。

示例 1：

输入：head = [1,2,3,4,5], left = 2, right = 4
输出：[1,4,3,2,5]
 
提示：

链表中节点数目为 n
1 <= n <= 500
-500 <= Node.val <= 500
1 <= left <= right <= n

 

进阶： 你可以使用一趟扫描完成反转吗？
```

## 思路
用头插法和虚拟头结点，一趟扫描完成反转

## 关键点
注释
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
    public ListNode reverseBetween(ListNode head, int left, int right) {
        //头插法
        //这里使用虚拟头结点，因为可能头结点就是反转开始的节点，不用虚拟头结点
        //就没办法在头结点前插入节点
        ListNode dummyHead = new ListNode(-1);
        dummyHead.next = head;

        ListNode g = dummyHead;
        ListNode p = dummyHead.next;

        for (int i = 0; i < left - 1; ++i) {
            g = g.next;
            p = p.next;
        }

        //right - left + 1是范围内所有节点个数，
        //而只需要把P节点后面的 right - left个节点头插即可
        for (int i = 0; i < right - left; ++i) {
            ListNode remove = p.next;
            p.next = p.next.next;
            remove.next = g.next;
            g.next = remove;
        }
        return dummyHead.next;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$


