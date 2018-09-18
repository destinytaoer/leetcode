# 实现 strStr\(\) 函数

## 描述

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 \(从0开始\)。如果不存在，则返回  **-1**。

**示例 1:**

```text
输入: haystack = "hello", needle = "ll"
输出: 2
```

**示例 2:**

```text
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

**说明:**

当 `needle` 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 `needle` 是空字符串时我们应当返回 0 。这与C语言的 strstr\(\) 以及 Java的 indexOf\(\) 定义相符。

## 实现

### 1. JavaScript 字符串原生方法 indexOf

没有思路，这是 JS 的原生实现

```javascript
var strStr = function(haystack, needle) {
  return haystack.indexOf(needle);
};
```

### 2. 循环加 substr 抽取比较

思路：

* 如果 needle 为空字符串，则返回 0
* 循环 haystack 字符串，如果当前项与 needle 的第一项相等
* 从当前项开始，抽取 haystack 字符串中，needle 长度的字符串
* 让这个抽取的字符串与 needle 比较，相等则符合，返回当前索引
* 不符合则继续循环，循环结束，没有返回则返回 -1

```javascript
var strStr = function(haystack, needle) {
  if (needle === '') return 0;
  for (let i = 0; i < haystack.length; i++) {
    let item = haystack[i];
    if (item === needle[0]) {
      let str = haystack.substr(i, needle.length);
      if (str === needle) return i;
    }
  }
  return -1;
};
```

{% hint style="info" %}
**优化：由于符合的子串应当长度相等，所以，最初的循环只需要到 haystack 长度 - needle 长度 + 1 即可，后面的子串长度肯定小于 needle，不需要考虑了**
{% endhint %}

```javascript
var strStr = function(haystack, needle) {
  if (needle === '') return 0;
  for (let i = 0; i < haystack.length - needle.length + 1; i++) {
    let item = haystack[i];
    if (item === needle[0]) {
      let str = haystack.substr(i, needle.length);
      if (str === needle) return i;
    }
  }
  return -1;
};
```

### 3. 双循环

思路：

* needle 为空字符串，返回 0
* 最笨的循环方式，循环 haystack，如果当前项与 needle 的第一项相等，则开始第二个循环
* 将 haystack 当前索引后面的字符与 needle 中的字符每个都进行比较，只要有一个不符合则退出循环
* 如果都符合，则返回当前索引
* 外层循环结束还是没有找到，则返回 -1

{% hint style="danger" %}
**注意**：这里提交，会显示时间超时，也就是两个字符串长度都很大的时候，两层循环，运行时间指数增长。

所以，为了减少循环次数，想到了上面方法中提到的优化，上面的方法也可以使用。优化后，代码运行时间就相当的可观了
{% endhint %}

```javascript
var strStr = function(haystack, needle) {
  if (needle === '') return 0;
  for (let i = 0; i < haystack.length-needle.length+1; i++) {
    let item = haystack[i];
    if (item === needle[0]) {
      let j = i+1,
          k = 1,
          flag = true;
      while (k < needle.length) {
        if (haystack[j] !== needle[k]) {
          flag = false;
          break;
        }
        j++;
        k++;
      }
      if (!flag) continue;
      return i;
    }
  }
  return -1;
};
```

