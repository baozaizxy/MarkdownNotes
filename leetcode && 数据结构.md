### leetcode && 数据结构

indice 索引

#### 指针pointer

遍历数组的过程中，可以使用双指针进行访问

相同方向--快慢指针： **通过两个指针以不同速度移动来解决问题**，一个指针（快指针）每次移动两步，另一个指针（慢指针）每次移动一步，快指针先到达目标或终点，慢指针用于定位关键位置。

反方向--对撞指针； **通过两个指针从数组两端向中间移动**，通常用于排序数组或字符串上的问题，比如二分查找、两数之和、判断回文等。一个指针从数组/字符串的左侧（起点）出发，另一个指针从数组/字符串的右侧（终点）出发，两个指针向中间移动，直到它们相遇。

双指针法用在涉及求和、比大小类的数组题目里时，大前提往往是：**该数组必须有序。**否则双指针根本无法帮助我们缩小定位的范围，压根没有意义。

**排序矩阵查找X**

给定 M×N 矩阵，每一行、每一列都按升序排列，请编写代码找出某元素。

解题思路：双指针，一个指针负责行，一个负责列，从右上角开始查找 时间复杂度 O(m+n)

1. **当前位置的值是所在行的最大值，同时是所在列的最小值**。
2. 从右上角的数开始查找，能够让每次判断都最大限度地排除一行或一列，从而逐步缩小搜索范围。

```js
// 示例:
// 现有矩阵 matrix 如下：
[
  [1, 4, 7, 11, 15],
  [2, 5, 8, 12, 19],
  [3, 6, 9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30],
];
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var searchMatrix = function (matrix, target) {
  const len = matrix.length;
  if (len === 0) {
    return false;
  }
  let rowIndex = 0;
  let colIndex = matrix[0].length - 1;
  while (rowIndex < len && colIndex >= 0) {
    if (matrix[rowIndex][colIndex] === target) {
      return true;
    } else if (matrix[rowIndex][colIndex] > target) {
      colIndex--;
    } else {
      rowIndex++;
    }
  }
  return false;
};
```

