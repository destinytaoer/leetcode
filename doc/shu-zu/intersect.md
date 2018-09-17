# 两个数组的交集 II

## 描述

给定两个数组，编写一个函数来计算它们的交集。

**示例 1:**

```text
输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2,2]
```

**示例 2:**

```text
输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出: [4,9]
```

**说明：**

* 输出结果中每个元素出现的次数，应与元素在两个数组中出现的次数一致。
* 我们可以不考虑输出结果的顺序。

**进阶:**

* 如果给定的数组已经排好序呢？你将如何优化你的算法？
* 如果 _nums1_ 的大小比 _nums2_ 小很多，哪种方法更优？
* 如果 _nums2_ 的元素存储在磁盘上，磁盘内存是有限的，并且你不能一次加载所有的元素到内存中，你该怎么办？

## 实现

### 1. 循环测试是否存在，存在则删除

思路：

* 先克隆一份需要操作的 nums2 数组
* 循环 nums1 数组
* 如果当前项在克隆的数组中已经存在，那么把当前项加入结果数组中，删除克隆数组中查找到的值（防止重复查找）

```javascript
/**
 * @param 
 *   nums1 [object] nums1 Array
 *   nums2 [object] nums2 Array
 * @return
 *   [Array]
 */
var intersect = function(nums1, nums2) {
  let ary = [...nums2],
      result = [];
  nums1.forEach(item=>{
    let index = ary.indexOf(item);
    if (index !== -1) {
      ary.splice(index,1);
      result.push(item);
    }
  })

  return result;
};
```

