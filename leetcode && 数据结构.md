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

#### 链表 linked list

链表和数组相似，它们都是有序的列表、都是线性结构（有且仅有一个前驱、有且仅有一个后继）。不同点在于，链表中，数据单位的名称叫做“**结点**”，而结点和结点的分布，在内存中可以是离散的。 在链表中，每一个结点的结构都包括了两部分的内容：数据域和指针域。**相对于数组来说，链表有一个明显的优点，就是添加和删除元素都不需要挪动多余的元素。**`JS` 中的链表，是以嵌套的对象的形式来实现的，`js` 原型链也是一个链表 ，沿着`__proto__` 特点：

- 多个元素组成列表
- 元素存储不连续，用 next 指针连在一起

```javascript
{
  // 数据域
  val: 1,
  // 指针域，指向下一个结点
  next: {
    val:2,
    next: ...
  }
}
  
// 需要一个构造函数
function ListNode(val) {
  this.val = val;
  this.next = null;
}

// 在使用构造函数创建结点时，传入 val （数据域对应的值内容）、指定 next （下一个链表结点）即可
const node = new ListNode(1);
node.next = new ListNode(2);
```

**链表的插入/删除效率较高 O(1)，而访问效率较低 O(n)；数组的访问效率较高 O(1)，而插入效率较低 O(n)。**

#### 集合 set

ES6中一种无序且唯一的数据结构集合，使用：去重，判断是否在集合中，求交集

// 增 const m = new Map(); m.set('a','aa'); // 查 m.get('a') // 'aa' // 删 m.delete('a') // 删除多有 m.clear();

```js
// 示例: 给定 nums = [2, 7, 11, 15], target = 9
// 因为 nums[0] + nums[1] = 2 + 7 = 9 所以返回 [0, 1]

/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
const twoSum = function (nums, target) {
  // 这里我用对象来模拟 map 的能力
  const diffs = {};
  // 缓存数组长度
  const len = nums.length;
  // 遍历数组
  for (let i = 0; i < len; i++) {
    // 判断当前值对应的 target 差值是否存在（是否已遍历过）
    if (diffs[target - nums[i]] > -1) {
      // 若有对应差值，那么答案get！
      return [diffs[target - nums[i]], i];
    }
    // 若没有对应差值，则记录当前值
    diffs[nums[i]] = i;
  }
  return [];
};
```

**采用空间换时间**：

常规解法双重循环，时间复杂度O(n^2)，空间复杂度O(1)

此解法，时间复杂度O(n)，空间复杂度O(n)



#### 树 Tree

树的常用操作：深度/广度优先遍历/先中后序遍历

| 方法        | 添加或移除 | 操作位置 | 返回值       | 是否修改原数组 | 时间复杂度 |
| ----------- | ---------- | -------- | ------------ | -------------- | ---------- |
| `shift()`   | 移除       | 开头     | 被移除的元素 | 是             | O(n)       |
| `unshift()` | 添加       | 开头     | 新的数组长度 | 是             | O(n)       |
| `push()`    | 添加       | 末尾     | 新的数组长度 | 是             | O(1)       |
| `pop()`     | 移除       | 末尾     | 被移除的元素 | 是             | O(1)       |

