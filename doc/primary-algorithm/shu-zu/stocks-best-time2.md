# 买卖股票的最佳时机 II

## 描述

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

**示例 1**:

```text
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
```

**示例 2**:

```text
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```

**示例 3**:

```text
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

## 实现

### 1. 循环前后两者比较

思路：

* 循环数组（不遍历最后一项），让当前项与后一项比较
* 如果当前项小于后一项，则购入当前项，然后在后一项的时候卖出
* 如果大于或等于，则什么也不做

```javascript
/**
* @param 
*   prices: [object] prices array
* @return 
*   [number] total
*/
var maxProfit = function(prices) {
let total = 0;
for (let i = 0; i < prices.length - 1; i++) {
  if (prices[i] < prices[i+1]) {
    total += prices[i+1] - prices[i];
  }
}
return total;
};
```

弊端：会产生连续购入和卖出

### 2. 优化循环比较

思路：

* 增加记录买入、卖出时的索引
* 增加比较，如果前一个不存在或者大于当前值，并且当前值小于后一个值，则记录当前索引为买入（此时实际买入），后一个索引为卖出索引（只是记录可能卖出，不是实际卖出）
* 如果前一个小于当前值，且当前值小于后一个值，则只记录后一个索引为卖出索引
* 如果当前值大于后一个值，则比较记录的两个买入、卖出索引值，不相等，则进行实际卖出，计算入收益，然后让买入索引（可能）变为卖出索引
* 在循环之后，仍然进行上一步操作，防止递增的数组退出循环，没有实际卖出

```javascript
var maxProfit = function(prices) {
  let total = 0,
      purchase = 0, // 记录买入
      sellOut = 0; // 记录卖出

  for (let i = 0; i < prices.length - 1; i++) {
    //=> 记录买入索引和卖出索引，此时实际买入
    if ((typeof prices[i-1] === 'undefined' || prices[i-1] >= prices[i]) && prices[i] < prices[i+1]) {
      purchase = i;
      sellOut = i + 1;
      continue;

    //=> 更新卖出索引的情况
    } else if(prices[i-1] < prices[i] && prices[i] < prices[i+1]) {
      sellOut = i + 1;
      continue;
    }
    //=> 实际卖出
    if (purchase !== sellOut) {
      total += prices[sellOut] - prices[purchase];
      purchase = sellOut;
    }
  }
  //=> 防止递增数组退出循环，没有进行实际卖出
  if (purchase !== sellOut) {
    total += prices[sellOut] - prices[purchase];
    purchase = sellOut;
  }
  return total;
};
```

