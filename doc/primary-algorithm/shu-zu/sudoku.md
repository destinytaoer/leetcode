# 有效的数独

## 描述

判断一个 9x9 的数独是否有效。只需要**根据以下规则**，验证已经填入的数字是否有效即可。

1. 数字 `1-9` 在每一行只能出现一次。
2. 数字 `1-9` 在每一列只能出现一次。
3. 数字 `1-9` 在每一个以粗实线分隔的 `3x3` 宫内只能出现一次。

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

上图是一个部分填充的有效的数独。

数独部分空格内已填入了数字，空白格用 `'.'` 表示。

**示例 1:**

```text
输入:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
输出: true
```

**示例 2:**

```text
输入:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
输出: false
解释: 除了第一行的第一个数字从 5 改为 8 以外，空格内其他数字均与 示例1 相同。
     但由于位于左上角的 3x3 宫内有两个 8 存在, 因此这个数独是无效的。
```

**说明:**

* 一个有效的数独（部分已被填充）不一定是可解的。
* 只需要根据以上规则，验证已经填入的数字是否有效即可。
* 给定数独序列只包含数字 `1-9` 和字符 `'.'` 。
* 给定数独永远是 `9x9` 形式的。

## 实现

### 1. 双循环加中间数组

思路：

* 分开横、竖以及1、2... 等九个格子进行判断
* 循环这几种类型，定义一个中间数组，每次循环一横、一竖或者一个格子时，都进行判断
* 如果当前项是 `.`，或者不是且在中间数组中不存在，则添加进中间数组
* 否则，就是出现了重复，那么直接返回 `false`
* 每次循环完一横、一竖或者一个格子时，就把中间数组清空，来进行重复利用
* 最后，循环结束都没有返回，那么说明数独有效，返回 `true`

```javascript
/**
 * @param
 *   board [object] Sudoku Array
 * @return
 *   [boolean]
 */
var isValidSudoku = function(board) {
  let n = board.length,
    ary = [];
  //=> 横
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      let item = board[i][j];
      if (item === '.' || (item !== '.' && ary.indexOf(item) === -1)) {
        ary.push(item);
      } else {
        return false;
      }
    }
    ary = [];
  }
  
  //=> 竖
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      let item = board[j][i];
      if (item === '.' || (item !== '.' && ary.indexOf(item) === -1)) {
        ary.push(item);
      } else {
        return false;
      }
    }
    ary = [];
  }
  
  //=> 1
  for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
      let item = board[i][j];
      if (item === '.' || (item !== '.' && ary.indexOf(item) === -1)) {
        ary.push(item);
      } else {
        return false;
      }
    }
  }
  ary = [];
  //=> 2
  for (let i = 3; i < 6; i++) {
    for (let j = 0; j < 3; j++) {
      let item = board[i][j];
      if (item === '.' || (item !== '.' && ary.indexOf(item) === -1)) {
        ary.push(item);
      } else {
        return false;
      }
    }
  }
  ary = [];
  //=> 3
  for (let i = 6; i < 9; i++) {
    for (let j = 0; j < 3; j++) {
      let item = board[i][j];
      if (item === '.' || (item !== '.' && ary.indexOf(item) === -1)) {
        ary.push(item);
      } else {
        return false;
      }
    }
  }
  ary = [];
  //=> 4
  for (let i = 0; i < 3; i++) {
    for (let j = 3; j < 6; j++) {
      let item = board[i][j];
      if (item === '.' || (item !== '.' && ary.indexOf(item) === -1)) {
        ary.push(item);
      } else {
        return false;
      }
    }
  }
  ary = [];
  //=> 5
  for (let i = 3; i < 6; i++) {
    for (let j = 3; j < 6; j++) {
      let item = board[i][j];
      if (item === '.' || (item !== '.' && ary.indexOf(item) === -1)) {
        ary.push(item);
      } else {
        return false;
      }
    }
  }
  ary = [];
  //=> 6
  for (let i = 6; i < 9; i++) {
    for (let j = 3; j < 6; j++) {
      let item = board[i][j];
      if (item === '.' || (item !== '.' && ary.indexOf(item) === -1)) {
        ary.push(item);
      } else {
        return false;
      }
    }
  }
  ary = [];
  //=> 7
  for (let i = 0; i < 3; i++) {
    for (let j = 6; j < 9; j++) {
      let item = board[i][j];
      if (item === '.' || (item !== '.' && ary.indexOf(item) === -1)) {
        ary.push(item);
      } else {
        return false;
      }
    }
  }
  ary = [];
  //=> 8
  for (let i = 3; i < 6; i++) {
    for (let j = 6; j < 9; j++) {
      let item = board[i][j];
      if (item === '.' || (item !== '.' && ary.indexOf(item) === -1)) {
        ary.push(item);
      } else {
        return false;
      }
    }
  }
  ary = [];
  //=> 9
  for (let i = 6; i < 9; i++) {
    for (let j = 6; j < 9; j++) {
      let item = board[i][j];
      if (item === '.' || (item !== '.' && ary.indexOf(item) === -1)) {
        ary.push(item);
      } else {
        return false;
      }
    }
  }
  return true;
};
```

