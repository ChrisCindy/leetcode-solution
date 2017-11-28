# Median of Two Sorted Arrays

## 问题描述
There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

Example 1:
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
Example 2:
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5

## 个人思路
### 利用 JS 内建函数完成两个数组合并为一个有序数组，然后取中位数

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var findMedianSortedArrays = function(nums1, nums2) {
    var finalArr = nums1.concat(nums2).sort(function(a,b){
        return a-b;
    });
    var len = finalArr.length;
    if (len % 2 === 0) {
        return (finalArr[len/2] + finalArr[len/2 - 1]) / 2;
    } else {
        return finalArr[(len-1)/2];
    }
};
```

### 总结

其实这里走了捷径，利用了内建函数避免了自己去实现两个数组的合并排序，具体的底层数组排序算法各个浏览器实现不同，不一定能够满足 o(log(m+n)) 的复杂度，如有时间还是应该自己实现一下。

## 优秀解法

都是从中位数的定义入手，偏算法层面解决、
// TODO: 待添加
