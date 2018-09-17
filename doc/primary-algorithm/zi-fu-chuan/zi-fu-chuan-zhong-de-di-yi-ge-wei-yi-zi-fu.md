# 字符串中的第一个唯一字符

## 描述

给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

**案例:**

```text
s = "leetcode"
返回 0.

s = "loveleetcode",
返回 2.
```

**注意事项：**您可以假定该字符串只包含小写字母。

## 实现

### 1. 前后出现索引是否一致

思路：

* 从开始往后循环字符串
* 判断当前字符在字符串中前后出现的索引是否一致
* 一致则没有重复，返回当前字符索引
* 不一致则继续循环
* 如果循环结束都没有返回值，则返回 -1

```javascript
/**
 * @param
 *   s [string]
 * @return 
 *   [number] index
 */
var firstUniqChar = function(s) {
  //=> 如果大小写算作重复的话
  s = s.toLowerCase();
  
  for (let i = 0; i < s.length; i++) {
    let item = s[i];
    if (s.indexOf(item) === s.lastIndexOf(item)) {
      return i;
    }
  }
  return -1;
};
```

### 2. 双循环

思路：

* 循环字符串，让每个字符都与字符串中的其它字符进行比较
* 如果存在重复的，那么后面就不需要再继续比较了，直接跳出里层循环，继续下一次外层循环
* 外层循环中需要进行标记，记录是否存在重复，如果不存在，则直接返回这个索引，结束函数
* 最后所有循环都结束还没有返回，则返回 -1

```javascript
var firstUniqChar = function(s) {
  //=> 如果大小写算作重复的话
  s = s.toLowerCase();
  
  for (let i = 0; i < s.length; i++) {
    //=> 记录是否存在重复，true 为不存在重复
    let flag = false;
    for (let j = 0; j < s.length; j++) {
      if (j !== i && s[i] === s[j]) {
        flag = true;
        break;
      }
    }
    if (!flag) {
      return i;
    }
  }
  return -1;
};
```

