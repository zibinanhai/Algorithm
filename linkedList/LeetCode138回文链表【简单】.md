
## 题目地址(234. 回文链表)

https://leetcode-cn.com/problems/palindrome-linked-list/

## 题目描述

```
请判断一个链表是否为回文链表。

示例 1:

输入: 1->2
输出: false

示例 2:

输入: 1->2->2->1
输出: true


进阶：
你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？
```

## 思路
* 先用快慢指针，慢指针边走边反转链表
* 慢指针走到链表中间时，根据链表节点个数是奇数还是偶数，来往两边遍历看是否相等

## 关键点
* 快慢指针一定要快指针先走，慢指针再反转，否则快指针就走回去了
* 判断奇数偶数处理的时候要画图
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
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) return true;
        //三个指针，两个慢指针一个快指针
        //快慢指针找到中点，慢指针在走到中点前 边走边反转
        ListNode pre = null, slow = head, fast = head, next = head;
        while (fast != null && fast.next != null) {
            //fast先行，再反转前面的，否则fast走回去了
            fast = fast.next.next;

            next = slow.next;
            slow.next = pre;
            pre = slow;
            slow = next;
        }
        ListNode left = pre;
        //偶数就两边比，奇数就去掉中间位置的往两边比
        //这一句比较关键，一定要在纸上确定奇数偶数和遍历的关系，模拟一下
        ListNode right = fast == null ? slow : slow.next;
        while (left != null && right != null) {
            if (left.val != right.val) {
                return false;
            }
            left = left.next;
            right = right.next;
        }
        return true;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$


