# Title
ZigZag Conversion

## 问题描述
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P   A   H   N
A P L S I I G
Y   I   R
And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:

string convert(string text, int nRows);
convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

## 个人思路
找规律，第一行和最后一行，字母在原字符的下标间隔为 interval = 2 * numRows - 2; 中间的 n 行，设当前行数为 i, 下标之间的间隔依次为 interval- 2 * (i - 1), 2 * (i -1), interval- 2 * (i - 1), 2 * (i -1), ...

```js
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function(s, numRows) {
  if (numRows === 1) {
    return s;
  } else {
    var result = '';
    var interval = 2 * numRows - 2;
    // 第 1 行
    var count = 0;
    while (s[count]) {
      result += s[count];
      count += interval;
    }
    // 第 2~(n-1)行
    for (var i = 2; i <= numRows - 1; i++) {
      count = i - 1;
      var oddFlag = true;
      while(s[count]) {
        console.log(s[count]);
        result += s[count];     
        count = count + (oddFlag ? interval - 2 * (i-1) : 2 * (i-1));
        oddFlag = !oddFlag;
      }
    }
    // 第 n 行
    count = numRows - 1;
    while(s[count]) {
      result += s[count];
      count += interval;
    }
    return result;
  }
};
```

### 总结
找规律题目，有点像脑筋急转弯

## 优秀解法
