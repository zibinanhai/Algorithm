
## 题目地址(61. 旋转链表)

https://leetcode-cn.com/problems/rotate-list/

## 题目描述

```
给你一个链表的头节点 head ，旋转链表，将链表每个节点向右移动 k 个位置。

 

示例 1：

输入：head = [1,2,3,4,5], k = 2
输出：[4,5,1,2,3]


提示：

链表中节点的数目在范围 [0, 500] 内
-100 <= Node.val <= 100
0 <= k <= 2 * 109
```

## 思路

## 关键点
* 关键点就是先有三个判空，如果是k = 0就直接返回head
* 还有一点就是K是长度的倍数的时候要直接返回，否则tail.next就会有环
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
    public ListNode rotateRight(ListNode head, int k) {
        if (k == 0 || head == null || head.next == null) {
            return head;
        }
        ListNode itr = head;
        int length = 0;
        while (itr != null) {
            itr = itr.next;
            length++;
        }
        int newIndex = length - k % length;
        ListNode pre = head;
        while (--newIndex != 0) {
            pre = pre.next;
        }
        ListNode tail = pre;
        if (pre.next == null) {
            return head;
        }
        ListNode res = pre.next;
//要遍历到最后一个节点而不是最后一个节点的next,就用这种方式遍历
        while (tail.next != null) {
            tail = tail.next;
        }
        pre.next = null;
//如果是链表是原地没变，一定要在前面判断返回，否则这里tail.next变成head就会有环
//或者和上一句代码换个位置
        tail.next = head;
        return res;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


