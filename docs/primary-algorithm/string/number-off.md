# 报数

## 描述

报数序列是指一个按照其中**的整数的**顺序进数序列，按行报数，得到下一个数。其前五项如下：

```text
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

`1` 被读作  `"one 1"`  \(`"一个一"`\) , 即 `11`。  
`11` 被读作 `"two 1"` \(`"两个一"`）, 即 `21`。  
`21` 被读作 `"one 2"`,  "`one 1"` （`"一个二"` ,  `"一个一"`\) , 即 `1211`。

给定一个正整数 _n_（1 ≤ _n_ ≤ 30），输出报数序列的第 _n_ 项。

注意：整数顺序将表示为一个字符串。

**示例 1:**

```text
输入: 1
输出: "1"
```

**示例 2:**

```text
输入: 4
输出: "1211"
```

## 实现

### 1. 利用正则以及替换

思路：

* 初始字符串为 `'1'`，那么后面循环次数应当是 n - 1
* 正则匹配所有连续的数字：`/1+|2+|3+|4+|5+|6+|7+|8+|9+/g`
* 把匹配的字符替换为长度加这个数字
* 循环完成后返回最后的字符串

```javascript
/**
 * @param
 *   n [number] number of times
 * @return
 *   [string] item n string
 */
var countAndSay = function(n) {
  let str = '1';
  let i = 1;
  let reg = /1+|2+|3+|4+|5+|6+|7+|8+|9+/g;
  while (i < n) {
    str = str.replace(reg, function(str) {
      let s = str.length + str[0];
      return s;
    })
    i++;
  }
  return str;
};
```



