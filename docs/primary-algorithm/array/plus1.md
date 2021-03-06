# 加一

## 描述

给定一个由**整数**组成的**非空**数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储一个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

**示例 1:**

```text
输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。
```

**示例 2:**

```text
输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。
```

## 实现

### 1. 字符串与数组相互转化方案

思路：

* 将数组转化为字符串
* 去掉字符串中的 , 号，变为组合成的数字字符串
* 再转化为数字，之后加1
* 再转化为字符串，然后逐位进行转化为数字后添加进数组中

但是，由于 JavaScript 中的整数运算，也有安全限制，具有最大安全计算值，超过这个值就会出错，所以，这个方法无法完全通过验证。

### 2. 从后往前循环加一

思路：

* 如果是原地算法，则直接操作参数即可，如果不是，则克隆一个数组，操作克隆数组即可
* 从后往前循环数组，进行加一操作
* 判断，如果加一后的数值小于 10，则循环结束
* 如果等于 10，则把当前索引的值赋值为 0，继续循环
* 如果等于 10 时，又已经到了第一个值，则向数组前面增加数字 1

```javascript
var plusOne = function(digits) {
  for (let i = digits.length-1; i >= 0; i--) {
    let temp = digits[i] + 1;
    
    if (temp === 10) {
      digits[i] = 0;
      if (i===0) {
        digits.unshift(1);
      }
      continue;
    }
    digits[i] = temp;
    break;
  }
  return digits;
};
```

