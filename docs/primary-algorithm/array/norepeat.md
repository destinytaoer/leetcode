# 排序数组去重

## 描述

给定一个**排序数组**，你需要在**原地**删除**重复**出现的元素，使得每个元素只出现一次，**返回移除后数组的新长度**。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 `O(1)` 额外空间的条件下完成。

**示例 1**:

```text
给定数组 nums = [1,1,2], 

函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 

你不需要考虑数组中超出新长度后面的元素。
```

**示例 2**:

```text
给定 nums = [0,0,1,1,1,2,2,3,3,4],

函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。

你不需要考虑数组中超出新长度后面的元素。
```

**说明**: 为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

```c
// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

## 实现

### 1. 使用对象存储

思路：

* 利用对象存储不重复的数字
* 循环数组，只要对象里面不存在该数字，则存储进去
* 如果已经存在，则在数组中利用索引删除该数字
* **需要注意数组的塌陷问题**

```javascript
/**
 * removeDuplicates
 * 
 * @param 
 *   nums [object] an Array
 * 
 * @return
 *   [number]: Array length
 */
var removeDuplicates = function(nums) {
  let obj = {};
  for (let i = 0; i < nums.length; i++) {
    if (obj.hasOwnProperty(nums[i])) {
       nums.splice(i, 1);
       i--;
       continue;
    }
    obj[nums[i]] = nums[i];
  }
  return nums.length;
};
```

### 2. 大小比较

思路：

* 由于其是排序后的数组，可以进行前后的大小比较
* 如果现在索引的数字等于后面的那个，则删除后面的数字
* 如果小于，则进行下一个循环
* 同样删除时注意数组塌陷问题

```javascript
var removeDuplicates = function(nums) {
  for (let i = 0; i < nums.length-1; i++) {
    if (typeof nums[i+1]!=='undefined' && nums[i] === nums[i+1]) {
      nums.splice(i+1, 1);
      i--;
      continue;
    }
  }
  return nums.length;
};
```

