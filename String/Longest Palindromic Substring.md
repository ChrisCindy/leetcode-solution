# Longest Palindromic Substring

## 问题描述
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example:

Input: "babad"

Output: "bab"

Note: "aba" is also a valid answer.
Example:

Input: "cbbd"

Output: "bb"

## 个人思路
### 

```js
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
    
};

function isPalindrome (str) {
  var len = str.length;
  var end;
  if (len % 2 === 0) {
    end = (len - 1) / 2;
  } else {
    end = len / 2;
  }

  for (var i = 0; i < end; i++) {
    if (str[i] !== str[len-1-i]) {
      return false;
    }    
  }
  return true;
}
```


### 总结


## 优秀解法

### 1. 
```java
public String longestPalindrome(String s) {
    int start = 0, end = 0;
    for (int i = 0; i < s.length(); i++) {
        int len1 = expandAroundCenter(s, i, i);
        int len2 = expandAroundCenter(s, i, i + 1);
        int len = Math.max(len1, len2);
        if (len > end - start) {
            start = i - (len - 1) / 2;
            end = i + len / 2;
        }
    }
    return s.substring(start, end + 1);
}

private int expandAroundCenter(String s, int left, int right) {
    int L = left, R = right;
    while (L >= 0 && R < s.length() && s.charAt(L) == s.charAt(R)) {
        L--;
        R++;
    }
    return R - L - 1;
}
```

### 2.
