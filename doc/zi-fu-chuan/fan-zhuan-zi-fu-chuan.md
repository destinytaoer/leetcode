# 反转字符串

## 描述

编写一个函数，其作用是将输入的字符串反转过来。

**示例 1:**

```text
输入: "hello"
输出: "olleh"
```

**示例 2:**

```text
输入: "A man, a plan, a canal: Panama"
输出: "amanaP :lanac a ,nalp a ,nam A"
```

## 实现

### 1. 转换为数组进行反转

思路：

* 先转化为数组
* 使用数组的反转方法进行反转
* 再转换为字符串返回

```javascript
/**
 * @param
 *   s [string]
 * @return 
 *   [string]
 */
var reverseString = function(s) {
  let ary = s.split('');
  ary.reverse();
  return ary.join('');
};
```

### 2. 从后往前循环每个字符

思路：

* 创建新字符串，从后往前循环每个字符
* 让当前字符拼接进创建的字符串中
* 返回创建的字符串

```javascript
var reverseString = function(s) {
  let str = '',
      i = s.length-1;
  while (i>=0) {
    str += s[i];
    i--;
  }
  return str;
};
```

