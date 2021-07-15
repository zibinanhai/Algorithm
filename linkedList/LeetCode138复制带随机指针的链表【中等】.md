
## 题目地址(138. 复制带随机指针的链表)

https://leetcode-cn.com/problems/copy-list-with-random-pointer/

## 题目描述

```
给你一个长度为 n 的链表，每个节点包含一个额外增加的随机指针 random ，该指针可以指向链表中的任何节点或空节点。

构造这个链表的 深拷贝。 深拷贝应该正好由 n 个 全新 节点组成，其中每个新节点的值都设为其对应的原节点的值。新节点的 next 指针和 random 指针也都应指向复制链表中的新节点，并使原链表和复制链表中的这些指针能够表示相同的链表状态。复制链表中的指针都不应指向原链表中的节点 。

例如，如果原链表中有 X 和 Y 两个节点，其中 X.random --> Y 。那么在复制链表中对应的两个节点 x 和 y ，同样有 x.random --> y 。

返回复制链表的头节点。

用一个由 n 个节点组成的链表来表示输入/输出中的链表。每个节点用一个 [val, random_index] 表示：

val：一个表示 Node.val 的整数。
random_index：随机指针指向的节点索引（范围从 0 到 n-1）；如果不指向任何节点，则为  null 。

你的代码 只 接受原链表的头节点 head 作为传入参数。

 

示例 1：

输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]


示例 2：

输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]


示例 3：

输入：head = [[3,null],[3,0],[3,null]]
输出：[[3,null],[3,0],[3,null]]


示例 4：

输入：head = []
输出：[]
解释：给定的链表为空（空指针），因此返回 null。


 

提示：

0 <= n <= 1000
-10000 <= Node.val <= 10000
Node.random 为空（null）或指向链表中的节点。
```



## 公司
* 字节 外企

- 暂无

## 思路
* 分两次遍历
* 第一次遍历用一个hashMap存各个节点对应的index，并建立一个新的链表，还要在List存入新节点
* 第二次遍历根据原链表的random，在map里面找到索引，并在List里根据索引找到对应新节点

## 关键点
* 注意处理random为Null的情况
* 注意两个itr都要往前走
* 要以Node为key，这样找random对应索引只需要第二次遍历就可以取到
-  

## 代码

- 语言支持：Java

Java Code:

```java

/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/

class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) {
            return null;
        }
        Node itr = head;
        Map<Node, Integer> map = new HashMap<>();
        List<Node> newCopy = new ArrayList<>();
        Node dummy = new Node(-1);
        Node newItr = dummy;
        //第一次遍历
        for (int i = 0; itr != null; ++i) {
            map.put(itr, i);
            Node node = new Node(itr.val);
            newItr.next = node;
            newCopy.add(node);
            itr = itr.next;
            newItr = newItr.next;
        }
        newItr = dummy.next;
        itr = head;
        //第二次遍历
        for (int i = 0; itr != null; ++i) {
            Node node = itr.random == null ? null : newCopy.get(map.get(itr.random));
            newItr.random = node == null ? null : node;
            itr = itr.next;
            newItr = newItr.next;
        }
        return dummy.next;   
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


