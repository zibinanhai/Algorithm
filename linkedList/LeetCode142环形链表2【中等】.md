
## 题目地址(142. 环形链表 II)

https://leetcode-cn.com/problems/linked-list-cycle-ii/

## 题目描述

```
给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。注意，pos 仅仅是用于标识环的情况，并不会作为参数传递到函数中。

说明：不允许修改给定的链表。

进阶：

你是否可以使用 O(1) 空间解决此题？

 

示例 1：

输入：head = [3,2,0,-4], pos = 1
输出：返回索引为 1 的链表节点
解释：链表中有一个环，其尾部连接到第二个节点。
 

提示：

链表中节点的数目范围在范围 [0, 104] 内
-105 <= Node.val <= 105
pos 的值为 -1 或者链表中的一个有效索引
```

- 暂无

## 思路
* 快慢指针，相遇很简单，关键是相遇后怎么找到入环点，入环点需要数学推导一下

## 关键点
1.  要推导，首先要知道slow在第一圈一定会碰见fast：
* 假设，slow进环的时候，fast和slow的距离为x（fast追slow的距离），
slow,每走一步，就被fast追上一步，所以slow走x步，就会相遇
* 由于这个x一定是小于一圈的，所以第一圈就会被追上

2. 接下来找这几段距离的关系：
* 假设head到入环点为a, 入环点到相遇点为b, 相遇点再顺时针到入环点为c
* 相遇时 slow: a + b
* fast: a + b + n(b + c)
* 根据2(a + b) = a + b + n (b + c)  -> a = n ( b + c) - b
* a = n (b + c) - b + c - c -> a = (n - 1) ( b + c) + c
* 结论就是从head到入环点的距离 等于相遇点到入环点 加n圈
* 所以这个时候用一个指针从head和slow(相遇点)一起走，一定会在入环点相遇
-  

## 代码

- 语言支持：Java

Java Code:

```java

/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode fast = head, slow = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                ListNode res = head;
                while(res != slow) {
                    res = res.next;
                    slow = slow.next;
                }
                return res;
            }
        }
        return null;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$


