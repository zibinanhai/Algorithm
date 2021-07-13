
## 题目地址(19. 删除链表的倒数第 N 个结点)

https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/

## 题目描述

```
给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。

进阶：你能尝试使用一趟扫描实现吗？

 

示例 1：

输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
 

提示：

链表中结点的数目为 sz
1 <= sz <= 30
0 <= Node.val <= 100
1 <= n <= sz
```

## 关键点
* 快慢指针
* 关键是处理删除的点正好是头结点的情况
* 可以用dummy来处理，也可以像代码特殊判断一下处理
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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) return head;

        ListNode fast = head, slow = head;
        for (int i = 0; i < n; ++i) {
            fast = fast.next;
        }
        if (fast == null) {
            //fast == null说明要删除的是头结点
            return head.next;
        }
        while (fast.next != null) {
            fast = fast.next;
            slow = slow.next;
        }
        ListNode removed = slow.next;
        slow.next = removed.next;
        removed.next = null;
        return head;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$


