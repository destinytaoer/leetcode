# 数组是否存在重复

## 描述

给定一个整数数组（没有排序），判断是否存在重复元素。

如果任何值在数组中出现至少两次，函数返回 `true`。如果数组中每个元素都不相同，则返回 `false`。

**示例 1**:

```text
输入: [1,2,3,1]
输出: true
```

**示例 2**:

```text
输入: [1,2,3,4]
输出: false
```

**示例 3**:

```text
输入: [1,1,1,3,3,4,3,2,4,2]
输出: true
```

## 实现

### 1. 前后出现的索引是否一致

思路：

* 循环数组，在数组中查找当前项索引
* 从前查找和从后查找索引是否一致
* 一致则没有重复，不一致则有重复

```javascript
/**
 * @param
 *   nums [object] nums Array
 * @return 
 *   [boolean]
 */
var containsDuplicate = function(nums) {
  for (let i = 0; i < nums.length; i++) {
    if (nums.indexOf(nums[i]) !== nums.lastIndexOf(nums[i])) {
      return true;
    }
  }
  return false;
};
```

### 2. 双循环

思路：

* 循环数组中的每一项（除去最后一项）
* 当前项与后面的每一项进行比较，相等则返回 `true`
* 循环结束都没有返回 `true`，证明没有重复，则返回 `false`

```javascript
var containsDuplicate = function(nums) {
  //=> 不用循环最后一项
  for (let i = 0; i < nums.length - 1; i++) {
    for (let j = i+1; j < nums.length; j++) {
      if (nums[i] === nums[j]) {
        return true;
      }
    }
  }
  return false;
};
```

### 3. 排序后，前后比较

思路：

* 克隆数组，防止改变原先数组
* 对克隆数组进行排序
* 循环克隆数组，让当前项与其前后两项进行比较（如果存在）
* 只要有一个相等，就返回 `true`
* 循环结束都没有返回，则说明没有重复，返回 `false`

```javascript
var containsDuplicate = function(nums) {
  let arr = [...nums];

  arr.sort((a, b)=>{
    return a - b;
  });

  for (let i = 0; i < arr.length; i++) {
    if ((typeof arr[i-1] !== 'undefined' && arr[i] === arr[i-1]) || (typeof arr[i+1] !== 'undefined' && arr[i] === arr[i+1])) {
      return true;
    }
  }
  return false;
};
```

