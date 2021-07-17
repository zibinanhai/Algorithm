
## 题目地址(25. K 个一组翻转链表)

https://leetcode-cn.com/problems/reverse-nodes-in-k-group/

## 题目描述

```
给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。

k 是一个正整数，它的值小于或等于链表的长度。

如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

进阶：

你可以设计一个只使用常数额外空间的算法来解决此问题吗？
你不能只是单纯的改变节点内部的值，而是需要实际进行节点交换。

 

示例 1：

输入：head = [1,2,3,4,5], k = 2
输出：[2,1,4,3,5]


示例 2：

输入：head = [1,2,3,4,5], k = 3
输出：[3,2,1,4,5]


示例 3：

输入：head = [1,2,3,4,5], k = 1
输出：[1,2,3,4,5]


示例 4：

输入：head = [1], k = 1
输出：[1]


提示：

列表中节点的数量在范围 sz 内
1 <= sz <= 5000
0 <= Node.val <= 1000
1 <= k <= sz
```

## 前置知识

- 

## 公司
* 字节 腾讯 外企

## 思路
* 其实就是多个翻转中间链表 合起来
* 记录好翻转的前驱后继即可
* pre -> start ... end -> next   其中pre 和 end 在外面定义，其他两个局部变量直接赋值

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
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || head.next == null) {
            return head;
        }
        //用pre 和 next记录翻转链表的前驱节点和后继节点
        //start和end记录翻转链表的头和尾部
        //顺序是 pre start ... end next，其中只需要定义pre和end，
        //另外两个每次翻转的时候用局部变量赋值即可
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode pre = dummy;
        ListNode end = dummy;

        //end.next不为null才说明这次翻转完还有后续结点，继续下一次尝试翻转
        while (end.next != null) {
            for (int i = 0; i < k && end != null; ++i) {
                end = end.next;
            }
            //结点不够K,结束翻转
            if (end == null) {
                break;
            }
            ListNode start = pre.next;
            ListNode next = end.next;
            
            //切断联系
            end.next = null;
            //翻转后和前驱后继节点连接
            pre.next = reverse(start);
            start.next = next;

            //恢复节点为下一次翻转做准备
            pre = start;
            end = start;
        }
        return dummy.next;
    }

    //翻转并返回新的链表头
    private ListNode reverse(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode pre = null;
        ListNode cur = head;
        while (cur != null) {
            //记联系方式
            ListNode next = cur.next;
            //翻转
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


