# 合并两个有序链表

## 描述

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

**示例：**

```text
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

## 实现

### 1. 依次排序，节点排序

思路：

* 如果 l1 或 l2 其中一个为空，则直接返回另一个
* 判断 l1 和 l2 的值哪一个大，那么就把头节点指向哪一个，同时，那一个链表往下移一位，并记录当前节点为头节点
* 循环，如果 l1 和 l2 都存在，则继续判断其值大小，将大的作为当前节点的下一个节点，当前节点置为其下一个节点，直到其中一个不存在为止
* 循环结束后，l1 或 l2 其中一个为空，则当前节点的下一个节点指针指向另外一个，最后返回头节点

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param
 *   l1 [object] ListNode
 *   l1 [object] ListNode
 * @return
 *   [object] ListNode
 */
var mergeTwoLists = function(l1, l2) {
  if (!l1) return l2;
  if (!l2) return l1;

  let head = null,
      cur = null;
  if (l1.val > l2.val) {
    head = l2;
    l2 = l2.next;
  } else {
    head = l1;
    l1 = l1.next;
  }
  cur = head;
  while (l1 && l2) {
    if (l1.val > l2.val) {
      cur.next = l2;
      l2 = l2.next;
    } else {
      cur.next = l1;
      l1 = l1.next;
    }
    cur = cur.next;
  }
  if (!l1) cur.next = l2;
  if (!l2) cur.next = l1;
  return head;
};
```

### 2. 利用数组排序，值排序

思路：

* 如果 l1 或 l2 其中一个为空，则直接返回另一个
* 将 l1 和 l2 直接拼接为新的链表
* 循环新的链表，将值保存在一个数组中
* 对数组进行排序
* 循环新的链表，将节点的值改为对应数组中的值，从而实现排序

```javascript
var mergeTwoLists = function(l1, l2) {
  if (!l1) return l2;
  if (!l2) return l1;

  let head = l1,
      ary = [];

  //=> 把所有值都保存在数组中
  ary.push(l1.val);
  while (l1.next) {
    l1 = l1.next;
    ary.push(l1.val);
  }
  l1.next = l2;
  while (l1.next) {
    l1 = l1.next;
    ary.push(l1.val);
  }

  //=> 对数组进行排序
  ary.sort((a,b)=>a-b);

  //=> 放回到新链表中
  l1 = head;
  ary.forEach(item=>{
    l1.val = item;
    l1 = l1.next;
  });
  return head;
};
```

