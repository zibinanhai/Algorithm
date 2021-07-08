
## 题目地址(2. 两数相加)

https://leetcode-cn.com/problems/add-two-numbers/

## 题目描述

```
给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。


示例 ：
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807. 
提示：

每个链表中的节点数在范围 [1, 100] 内
0 <= Node.val <= 9
题目数据保证列表表示的数字不含前导零
```

## 思路
* 这道题其实就是模仿加法运算，注意进位即可
## 关键点
* 不能先把两个数读出来相加，因为没有给出数的范围，可能不够存
* 只能按位来算，因为链表是逆序的，所以直接在链表尾部填0

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //其实就是模拟加法，因为是倒叙，只用在链表尾部补0即可
        ListNode head = null;
        ListNode tail = null;
        int carry = 0;
        while (l1 != null || l2 != null) {
            //只要有一个不为空，说明高位还有数字需要加
            int n1 = l1 == null ? 0 : l1.val;
            int n2 = l2 == null ? 0 : l2.val;
            if (head == null) {
                head = tail = new ListNode((n1 + n2 + carry) % 10);
            } else {
                tail.next = new ListNode((n1 + n2 + carry) % 10);
                tail = tail.next;
            }
            l1 = l1 == null ? null : l1.next;
            l2 = l2 == null ? null : l2.next;
            carry = (n1 + n2 + carry) / 10;
        }
        if (carry > 0) {
            tail.next = new ListNode(carry);
        }
        return head;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


