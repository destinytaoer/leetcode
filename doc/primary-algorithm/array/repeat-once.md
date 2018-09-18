# 获取数组中只出现一次的数字

## 描述

给定一个**非空**整数数组，除了某个元素**只出现一次**以外，其余每个元素均出现两次。找出那个**只出现了一次的元素**。

**说明**：

你的算法应该具有**线性时间复杂度**。 你可以**不使用额外空间**来实现吗？

**示例 1**:

```text
输入: [4,1,2,1,2]
输出: 4
```

## 实现

### 1. 利用前后出现的索引比较

思路：

* 循环数组，判断是否有重复，使用前后出现的索引比较
* 重复则继续
* 由于只有一个数字是出现一次的，把没有重复的那个返回即可

```javascript
/**
 * @param
 *   nums [object] nums Array
 * @return
 *   [number] single number
 */
var singleNumber = function(nums) {
  for (let i = 0; i < nums.length; i++) {
    if (nums.indexOf(nums[i]) === nums.lastIndexOf(nums[i])) {
      return nums[i];
    }
  }
};
```

### 2. 先排序后比较

思路：

* 克隆数组，防止改变原先数组
* 对克隆数组进行排序
* 循环克隆数组，让当前项与其前后两项进行比较
* 只要当前项与前后两项都不相等（不论是否存在），则该值就是需要返回的值

```javascript
var singleNumber = function(nums) {
  let arr = [...nums];
  arr.sort((a, b)=>{
    return a - b;
  });
  
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] !== arr[i-1] && arr[i] !== arr[i+1]) {
      return arr[i];
    }
  }
};
```

弊端：需要一个额外的空间存储数组

