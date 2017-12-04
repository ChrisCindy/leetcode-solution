# Title
Palindrome Number

## 问题描述
Determine whether an integer is a palindrome. Do this without extra space.

## 个人思路
### 

从分析来看，将数字转为字符串，可行但有额外空间，不符合题设；将数字全盘反转，再与自身比较，有溢出风险；折衷方案是将数字的后半部分反转，再与数字的前半部分对比。

此外，还掌握了通用的反转数字的方法：循环，按位取出（见代码的 while 部分）。
注意：js 的数字处理的坑。

```js
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
    if (x < 0 || (x % 10 === 0 && x !== 0)) {
      return false;
    }
    var revertedNumber = 0;
    while (x > revertedNumber) {
      revertedNumber = revertedNumber * 10 + x % 10;
      x = Math.floor(x/10);  
    }

    return x === revertedNumber || x === Math.floor(revertedNumber / 10);
};
```

### 总结


## 优秀解法
