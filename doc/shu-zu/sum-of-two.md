# 两数之和

## 描述

给定一个整数数组和一个目标值，找出数组中和为目标值的**两个**数。

你可以假设每个输入只对应一种答案，且同样的元素不能被重复利用。

**示例:**

```text
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

## 实现

### 1. 双循环

思路：

* 循环数组，将每一项（除最后一项外）都与其后面的所有项比较
* 如果两项相加等于目标值，则将两项的索引添加进结果数组中，然后退出循环
* 最后返回结果数组，不存在则返回空数组

```javascript
/**
 * @param
 *   nums [object] nums Array
 *   target [number] target number
 * @return {number[]}
 */
var twoSum = function(nums, target) {
  let ary = [];
  for (let i = 0; i < nums.length - 1; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        ary.push(i);
        ary.push(j);
        break;
      }
    }
  }
  return ary;
};
```

如果需要返回所有相加等于目标值的索引组合，那么就把索引组合成一个数组再添加进结果数组中，并且不退出循环。但是这样的话就会对元素重复利用。

