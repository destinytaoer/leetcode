# 字符串转整数（atoi）

## 描述

实现 `atoi`，将字符串转为整数。

在找到第一个非空字符之前，需要移除掉字符串中的空格字符。如果第一个非空字符是正号或负号，选取该符号，并将其与后面尽可能多的连续的数字组合起来，这部分字符即为整数的值。如果第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。

字符串可以在形成整数的字符后面包括多余的字符，这些字符可以被忽略，它们对于函数没有影响。

当字符串中的第一个非空字符序列不是个有效的整数；或字符串为空；或字符串仅包含空白字符时，则不进行转换。

若函数不能执行有效的转换，返回 0。

**说明：**

假设我们的环境只能存储 32 位有符号整数，其数值范围是 \[−231, 231 − 1\]。如果数值超过可表示的范围，则返回 INT\_MAX \(231 − 1\) 或 INT\_MIN \(−231\) 。

**示例 1:**

```text
输入: "42"
输出: 42
```

**示例 2:**

```text
输入: "   -42"
输出: -42
解释: 第一个非空白字符为 '-', 它是一个负号。
     我们尽可能将负号与后面所有连续出现的数字组合起来，最后得到 -42 。
```

**示例 3:**

```text
输入: "4193 with words"
输出: 4193
解释: 转换截止于数字 '3' ，因为它的下一个字符不为数字。
```

**示例 4:**

```text
输入: "words and 987"
输出: 0
解释: 第一个非空字符是 'w', 但它不是数字或正、负号。
     因此无法执行有效的转换。
```

**示例 5:**

```text
输入: "-91283472332"
输出: -2147483648
解释: 数字 "-91283472332" 超过 32 位有符号整数范围。 
     因此返回 INT_MIN (−231) 。
```

## 实现

### 1. 利用 parseInt 以及 isNaN

思路：

* 使用 parseInt 转换字符串
* 如果是 NaN，则将结果变为 0
* 进行结果的最大最小值限制

```javascript
/**
 * @param
 *   str [string]
 * @return
 *   [number] int
 */
var myAtoi = function(str) {
  let num = parseInt(str);
  if(isNaN(num)) {
    num = 0;
  }
  let max = (2**31)-1,
      min = -(2**31);
  num = num > max ? max : num;
  num = num < min ? min : num;
  return num;
};
```

### 2. 利用正则循环判断

思路：

* 先去空格
* 判断第一个字符是否是数字或者正负号，不是则返回 0
* 保存第一个字符串
* 循环字符串（从索引 1 开始），添加入结果字符中，遇到不是数字的跳出循环
* 如果第一个字符为正负号，且结果字符串为空，那么返回 0
* 否则，将正负号添加会结果字符串前面，并将结果字符串转化为数字
* 进行结果最大最小限制
* 返回结果数字

```javascript
var myAtoi = function(str) {
  str = str.trim();
  let reg = /^[0-9-+]/,
      max = (2**31)-1,
      min = -(2**31)
  if (!reg.test(str)) {
    return 0;
  }

  let num = '',
      c = str[0];
  for (let i = 1; i < str.length;i++) {
    if (!/[0-9]/.test(str[i])) {
      break;
    }
    num += str[i];
  }
  if ((c === '-' ||c === '+') && num.length === 0) return 0;
  num = (c + num)*1;
  num = num < min ? min : num;
  num = num > max ? max : num;
  return num;
};
```
