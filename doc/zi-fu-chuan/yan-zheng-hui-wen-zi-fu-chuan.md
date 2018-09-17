# 验证回文字符串

## 描述

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

**说明：**本题中，我们将空字符串定义为有效的回文串。

**示例 1:**

```text
输入: "A man, a plan, a canal: Panama"
输出: true
```

**示例 2:**

```text
输入: "race a car"
输出: false
```

## 实现

### 1. 利用正则替换和反转字符串

思路：

* 利用正则替换掉不是数字和字母的字符
* 由于忽略大小写，将其变为小写
* 反转字符串
* 将反转字符串和原字符串比较，相等则是回文，返回 `true`
* 否则返回 `false`

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function(s) {
  s = s.replace(/[^a-zA-Z0-9]/g, '').toLowerCase();
  let str = s.split('').reverse().join('');
  if (str === s) return true;
  return false;
};
```

### 2. 利用正则替换和折半比较

思路：

* 利用正则替换掉不是数字和字母的字符
* 由于忽略大小写，将其变为小写
* 算出需要的中间值（从左开始）
* 分别从左开始和从右开始循环比较，直到左边到达中间值为止
* 如果存在不相等的，则返回 `false`
* 循环结束都没有返回，则返回 `true`

```javascript
var isPalindrome = function(s) {
  s = s.replace(/[^0-9a-zA-Z]/g, '').toLowerCase();
  let mid = Math.floor(s.length/2)-1,
      i = 0,
      j = s.length - 1;
  while (i <= mid) {
    if (s[i] !== s[j]) {
      return false;
    }
    i++;
    j--;
  }
  return true;
};
```

