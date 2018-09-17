# 有效的字母异位词

## 描述

给定两个字符串 _s_ 和 _t_ ，编写一个函数来判断 _t_ 是否是 _s_ 的一个字母异位词。

**示例 1:**

```text
输入: s = "anagram", t = "nagaram"
输出: true
```

**示例 2:**

```text
输入: s = "rat", t = "car"
输出: false
```

**说明:**  
你可以假设字符串只包含小写字母。

**进阶:**  
如果输入字符串包含 unicode 字符怎么办？你能否调整你的解法来应对这种情况？

## 实现

### 1. 利用替换删除字符

思路：

* 循环第一个字符串，将第二个字符串中替换当前字符为空，即，如果当前字符在第二个字符串中存在，则删除，不存在，则什么也不干
* 循环结束后，如果第二个字符串中还有字符，则不是异位词，返回 `false`
* 否则返回 `true`

```javascript
/**
 * @param 
 *   s [string] first word
 *   t [string] second word
 * @return
 *   [boolean]
 */
var isAnagram = function(s, t) {
  //=> 如果长度不一样，直接返回 false
  if (s.length !== t.length) return false;
  for (let i = 0; i < s.length; i++) {
    t = t.replace(s[i], '');
  }
  if (t.length !== 0) {
    return false;
  }
  return true;
};
```

如果存在 Unicode 字符，利用正则，将其替换正常的字符（使用String.fromCodePoint\(\)）

