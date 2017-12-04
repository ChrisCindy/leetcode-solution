# Add Two Numbers

## 问题描述
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

## 个人思路
~~1. 将两个输入的链表获取并保存为数组，然后转换：数组 -> 字符串 -> 数字，相加后再逆序转换，最后保存为链表~~
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
  var arr1 = [], arr2 = [];
  do {
    var val1 = l1.val;
    arr1.push(val1);
    l1 = l1.next;
  }
  while (l1);
  do {
    var val2 = l2.val;
    arr2.push(val2);
    l2 = l2.next;
  }
  while (l2);
  var n1 = parseInt(arr1.reverse().join(''));
  var n2 = parseInt(arr2.reverse().join(''));
  var res = (n1 + n2).toString().split('').reverse().map(function(item){
    return new ListNode(parseInt(item));
  });
  for (var i = 0, j = res.length - 1; i < j; i++) {
    res[i].next = res[i+1];
  }
  return res[0];  
};
```

WA
分析：input 数组过大时无法存放大数，导致溢出。

2. 直接将两个链表，逐位相加，实时生成结果链表
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
  // l1 = reverseLink1(l1);
  // l2 = reverseLink1(l2);
  var head, temp, carry = 0, isHead = true, trueHead;
  while (l1 || l2 || carry) {
    var tempVal;
    var val1 = l1 ? l1.val : 0;
    var val2 = l2 ? l2.val : 0;    
    
    tempVal = val1 + val2 + carry;      
    
    if (tempVal >= 10) {
      carry = 1;
      tempVal %= 10;
    } else {
      carry = 0;
    }


    head = new ListNode(tempVal);
    if (isHead) {
      trueHead = head;
      isHead = false;
      temp = head;    
    }
    temp.next = head;
    temp = head;
    if (l1 || l2) {
      l1 = l1 ? l1.next : null;
      l2 = l2 ? l2.next : null;
    } else {
      break;
    }

  }
  head.next = null;
  return trueHead;
};

// 迭代
function reverseLink1 (head) {
  var next, prev = null;
  while(head !== null) {
    next = head.next;
    head.next = prev;
    prev = head;
    head = next;
  }
  return prev;
}

// 递归
function reverseLink2 (head) {
  var newHead;

  if ((head === null) || (head.next === null)) {
    return head;
  }

  newHead = reverseLink2(head.next);
  head.next.next = head;
  head.next = null;

  return newHead;
}
```

### 总结
其实这里智障了，本来根本不需要进行链表的逆序，但是也正好复习了单链表逆序的方法。

## 优秀解法
与个人理解一致。
