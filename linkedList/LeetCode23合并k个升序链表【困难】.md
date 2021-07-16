
## 题目地址(23. 合并K个升序链表)

https://leetcode-cn.com/problems/merge-k-sorted-lists/

## 题目描述

```
给你一个链表数组，每个链表都已经按升序排列。

请你将所有链表合并到一个升序链表中，返回合并后的链表。

 

示例 1：

输入：lists = [[1,4,5],[1,3,4],[2,6]]
输出：[1,1,2,3,4,4,5,6]
解释：链表数组如下：
[
  1->4->5,
  1->3->4,
  2->6
]
将它们合并到一个有序链表中得到。
1->1->2->3->4->4->5->6


示例 2：

输入：lists = []
输出：[]


示例 3：

输入：lists = [[]]
输出：[]


 

提示：

k == lists.length
0 <= k <= 10^4
0 <= lists[i].length <= 500
-10^4 <= lists[i][j] <= 10^4
lists[i] 按 升序 排列
lists[i].length 的总和不超过 10^4
```

## 前置知识

- 

## 公司
* 字节 外企
- 暂无

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
    //设链表最大长度为n, lists长度为k, 这个普通的迭代时间复杂度为O(k2n),太慢了
    // public ListNode mergeKLists(ListNode[] lists) {
    //     if (lists == null || lists.length == 0) {
    //         return null;
    //     }
    //     int first = 0;
    //     int index = 0;
    //     for (int i = 0; i < lists.length; ++i) {
    //         if (lists[i] != null) {
    //             first = lists[i].val;
    //             index = i;
    //             break;
    //         }
    //     }
    //     for (int i = 0; i < lists.length; ++i) {
    //         //lists的每一个元素都有可能为null
    //         if (lists[i] != null && lists[i].val < first) {
    //             first = lists[i].val;
    //             index = i;
    //         }
    //     }
    //     ListNode res = null;
    //     //递归边界  每一个list都为null
    //     if (lists[index] != null) {
    //         res = lists[index];
    //         lists[index] = lists[index].next;
    //         res.next = mergeKLists(lists);
    //     }
    //     return res;
    // }

    //第二个方法为优先队列，优先队列力放的是链表，根据链表的第一个节点的值哪个最小来设置优先级
    //每次poll后，更新当前链表，判断next不为null的时候把next放进去
    public ListNode mergeKLists(ListNode[] lists) {
        // 这里可以不需要，这两种情况优先队列都为空，直接输出null;
        //只不过加上执行速度会快一点
        if (lists == null || lists.length == 0) {
            return null;
        }
        PriorityQueue<ListNode> p = new PriorityQueue<>(new Comparator<ListNode>() {
            public int compare(ListNode n1, ListNode n2) {
                //优先队列返回负数就是第一个元素在前
                return n1.val - n2.val;
            }
        });
        ListNode dummy = new ListNode(-1);
        ListNode cur = dummy;

        //先把链表都放进去
        for (int i = 0; i < lists.length; ++i) {
            if (lists[i] != null) {
                p.offer(lists[i]);
            }
        }
        while (!p.isEmpty()) {
            cur.next = p.poll();
            cur = cur.next;
            if (cur.next != null) {
                p.offer(cur.next);
            }
        }
        return dummy.next;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：
* 设链表最大长度为n, lists长度为k
* 第一种方法的时间复杂度为O(k2n)
* 第二种方法由于优先队列poll的时间复杂度为log(N),所以 第二种方法的时间复杂度为O(nklog(k))


