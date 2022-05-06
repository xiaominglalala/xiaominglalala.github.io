---
layout:     post
title:      Exercise 4 (Just asy) 
subtitle:   
date:       2022-05-05
author:     Ethan
header-img: img/7.jpg
catalog: true
tags:
    - Leetcode

---

## Exercise 4 (Just Easy)

#### [1822. 数组元素积的符号](https://leetcode-cn.com/problems/sign-of-the-product-of-an-array/)

难度简单21

已知函数 `signFunc(x)` 将会根据 `x` 的正负返回特定值：

- 如果 `x` 是正数，返回 `1` 。
- 如果 `x` 是负数，返回 `-1` 。
- 如果 `x` 是等于 `0` ，返回 `0` 。

给你一个整数数组 `nums` 。令 `product` 为数组 `nums` 中所有元素值的乘积。

返回 `signFunc(product)` 。

 

**示例 1：**

```
输入：nums = [-1,-2,-3,-4,3,2,1]
输出：1
解释：数组中所有值的乘积是 144 ，且 signFunc(144) = 1
```

**示例 2：**

```
输入：nums = [1,5,0,2,-3]
输出：0
解释：数组中所有值的乘积是 0 ，且 signFunc(0) = 0
```

**示例 3：**

```
输入：nums = [-1,1,-1,1,-1]
输出：-1
解释：数组中所有值的乘积是 -1 ，且 signFunc(-1) = -1
```

 

**提示：**

- `1 <= nums.length <= 1000`
- `-100 <= nums[i] <= 100`

#### [1656. 设计有序流](https://leetcode-cn.com/problems/design-an-ordered-stream/)

难度简单21

有 `n` 个 `(id, value)` 对，其中 `id` 是 `1` 到 `n` 之间的一个整数，`value` 是一个字符串。不存在 `id` 相同的两个 `(id, value)` 对。

设计一个流，以 **任意** 顺序获取 `n` 个 `(id, value)` 对，并在多次调用时 **按 `id` 递增的顺序** 返回一些值。

实现 `OrderedStream` 类：

- `OrderedStream(int n)` 构造一个能接收 `n` 个值的流，并将当前指针 `ptr` 设为 `1` 。

- ```
  String[] insert(int id, String value)
  ```

   

  向流中存储新的

   

  ```
  (id, value)
  ```

   

  对。存储后：

  - 如果流存储有 `id = ptr` 的 `(id, value)` 对，则找出从 `id = ptr` 开始的 **最长 id 连续递增序列** ，并 **按顺序** 返回与这些 id 关联的值的列表。然后，将 `ptr` 更新为最后那个 `id + 1` 。
  - 否则，返回一个空列表。

 

**示例：**

**![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/q1.gif)**

```
输入
["OrderedStream", "insert", "insert", "insert", "insert", "insert"]
[[5], [3, "ccccc"], [1, "aaaaa"], [2, "bbbbb"], [5, "eeeee"], [4, "ddddd"]]
输出
[null, [], ["aaaaa"], ["bbbbb", "ccccc"], [], ["ddddd", "eeeee"]]

解释
OrderedStream os= new OrderedStream(5);
os.insert(3, "ccccc"); // 插入 (3, "ccccc")，返回 []
os.insert(1, "aaaaa"); // 插入 (1, "aaaaa")，返回 ["aaaaa"]
os.insert(2, "bbbbb"); // 插入 (2, "bbbbb")，返回 ["bbbbb", "ccccc"]
os.insert(5, "eeeee"); // 插入 (5, "eeeee")，返回 []
os.insert(4, "ddddd"); // 插入 (4, "ddddd")，返回 ["ddddd", "eeeee"]
```

 

**提示：**

- `1 <= n <= 1000`
- `1 <= id <= n`
- `value.length == 5`
- `value` 仅由小写字母组成
- 每次调用 `insert` 都会使用一个唯一的 `id`
- 恰好调用 `n` 次 `insert`

#### [1304. 和为零的N个唯一整数](https://leetcode-cn.com/problems/find-n-unique-integers-sum-up-to-zero/)

难度简单61

给你一个整数 `n`，请你返回 **任意** 一个由 `n` 个 **各不相同** 的整数组成的数组，并且这 `n` 个数相加和为 `0` 。

 

**示例 1：**

```
输入：n = 5
输出：[-7,-1,1,3,4]
解释：这些数组也是正确的 [-5,-1,1,2,3]，[-3,-1,2,-2,4]。
```

**示例 2：**

```
输入：n = 3
输出：[-1,0,1]
```

**示例 3：**

```
输入：n = 1
输出：[0]
```

 

**提示：**

- `1 <= n <= 1000`

#### [1636. 按照频率将数组升序排序](https://leetcode-cn.com/problems/sort-array-by-increasing-frequency/)

难度简单43

给你一个整数数组 `nums` ，请你将数组按照每个值的频率 **升序** 排序。如果有多个值的频率相同，请你按照数值本身将它们 **降序** 排序。 

请你返回排序后的数组。

 

**示例 1：**

```
输入：nums = [1,1,2,2,2,3]
输出：[3,1,1,2,2,2]
解释：'3' 频率为 1，'1' 频率为 2，'2' 频率为 3 。
```

**示例 2：**

```
输入：nums = [2,3,1,3,2]
输出：[1,3,3,2,2]
解释：'2' 和 '3' 频率都为 2 ，所以它们之间按照数值本身降序排序。
```

**示例 3：**

```
输入：nums = [-1,1,-6,4,5,-6,1,4,1]
输出：[5,-1,4,4,-6,-6,1,1,1]
```

 

**提示：**

- `1 <= nums.length <= 100`
- `-100 <= nums[i] <= 100`

#### 557. Reverse Words in a String III

Easy

2754164Add to ListShare

Given a string `s`, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

 

**Example 1:**

```
Input: s = "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```

**Example 2:**

```
Input: s = "God Ding"
Output: "doG gniD"
```

 

**Constraints:**

- `1 <= s.length <= 5 * 104`
- `s` contains printable **ASCII** characters.
- `s` does not contain any leading or trailing spaces.
- There is **at least one** word in `s`.
- All the words in `s` are separated by a single space.

#### 1640. Check Array Formation Through Concatenation

Easy

679113Add to ListShare

You are given an array of **distinct** integers `arr` and an array of integer arrays `pieces`, where the integers in `pieces` are **distinct**. Your goal is to form `arr` by concatenating the arrays in `pieces` **in any order**. However, you are **not** allowed to reorder the integers in each array `pieces[i]`.

Return `true` *if it is possible* *to form the array* `arr` *from* `pieces`. Otherwise, return `false`.

 

**Example 1:**

```
Input: arr = [15,88], pieces = [[88],[15]]
Output: true
Explanation: Concatenate [15] then [88]
```

**Example 2:**

```
Input: arr = [49,18,16], pieces = [[16,18,49]]
Output: false
Explanation: Even though the numbers match, we cannot reorder pieces[0].
```

**Example 3:**

```
Input: arr = [91,4,64,78], pieces = [[78],[4,64],[91]]
Output: true
Explanation: Concatenate [91] then [4,64] then [78]
```

 

**Constraints:**

- `1 <= pieces.length <= arr.length <= 100`
- `sum(pieces[i].length) == arr.length`
- `1 <= pieces[i].length <= arr.length`
- `1 <= arr[i], pieces[i][j] <= 100`
- The integers in `arr` are **distinct**.
- The integers in `pieces` are **distinct** (i.e., If we flatten pieces in a 1D array, all the integers in this array are distinct).

#### [1603. 设计停车系统](https://leetcode-cn.com/problems/design-parking-system/)

难度简单112

请你给一个停车场设计一个停车系统。停车场总共有三种不同大小的车位：大，中和小，每种尺寸分别有固定数目的车位。

请你实现 `ParkingSystem` 类：

- `ParkingSystem(int big, int medium, int small)` 初始化 `ParkingSystem` 类，三个参数分别对应每种停车位的数目。
- `bool addCar(int carType)` 检查是否有 `carType` 对应的停车位。 `carType` 有三种类型：大，中，小，分别用数字 `1`， `2` 和 `3` 表示。**一辆车只能停在** `carType` 对应尺寸的停车位中。如果没有空车位，请返回 `false` ，否则将该车停入车位并返回 `true` 。

 

**示例 1：**

```
输入：
["ParkingSystem", "addCar", "addCar", "addCar", "addCar"]
[[1, 1, 0], [1], [2], [3], [1]]
输出：
[null, true, true, false, false]

解释：
ParkingSystem parkingSystem = new ParkingSystem(1, 1, 0);
parkingSystem.addCar(1); // 返回 true ，因为有 1 个空的大车位
parkingSystem.addCar(2); // 返回 true ，因为有 1 个空的中车位
parkingSystem.addCar(3); // 返回 false ，因为没有空的小车位
parkingSystem.addCar(1); // 返回 false ，因为没有空的大车位，唯一一个大车位已经被占据了
```

 

**提示：**

- `0 <= big, medium, small <= 1000`
- `carType` 取值为 `1`， `2` 或 `3`
- 最多会调用 `addCar` 函数 `1000` 次

#### [696. 计数二进制子串](https://leetcode-cn.com/problems/count-binary-substrings/)

难度简单453

给定一个字符串 `s`，统计并返回具有相同数量 `0` 和 `1` 的非空（连续）子字符串的数量，并且这些子字符串中的所有 `0` 和所有 `1` 都是成组连续的。

重复出现（不同位置）的子串也要统计它们出现的次数。

**示例 1：**

```
输入：s = "00110011"
输出：6
解释：6 个子串满足具有相同数量的连续 1 和 0 ："0011"、"01"、"1100"、"10"、"0011" 和 "01" 。
注意，一些重复出现的子串（不同位置）要统计它们出现的次数。
另外，"00110011" 不是有效的子串，因为所有的 0（还有 1 ）没有组合在一起。
```

**示例 2：**

```
输入：s = "10101"
输出：4
解释：有 4 个子串："10"、"01"、"10"、"01" ，具有相同数量的连续 1 和 0 。
```

 

**提示：**

- `1 <= s.length <= 105`
- `s[i]` 为 `'0'` 或 `'1'`

#### [1710. 卡车上的最大单元数](https://leetcode-cn.com/problems/maximum-units-on-a-truck/)

难度简单34

请你将一些箱子装在 **一辆卡车** 上。给你一个二维数组 `boxTypes` ，其中 `boxTypes[i] = [numberOfBoxesi, numberOfUnitsPerBoxi]` ：

- `numberOfBoxesi` 是类型 `i` 的箱子的数量。
- `numberOfUnitsPerBoxi` 是类型 `i` 每个箱子可以装载的单元数量。

整数 `truckSize` 表示卡车上可以装载 **箱子** 的 **最大数量** 。只要箱子数量不超过 `truckSize` ，你就可以选择任意箱子装到卡车上。

返回卡车可以装载 **单元** 的 **最大** 总数*。*

 

**示例 1：**

```
输入：boxTypes = [[1,3],[2,2],[3,1]], truckSize = 4
输出：8
解释：箱子的情况如下：
- 1 个第一类的箱子，里面含 3 个单元。
- 2 个第二类的箱子，每个里面含 2 个单元。
- 3 个第三类的箱子，每个里面含 1 个单元。
可以选择第一类和第二类的所有箱子，以及第三类的一个箱子。
单元总数 = (1 * 3) + (2 * 2) + (1 * 1) = 8
```

**示例 2：**

```
输入：boxTypes = [[5,10],[2,5],[4,7],[3,9]], truckSize = 10
输出：91
```

 

**提示：**

- `1 <= boxTypes.length <= 1000`
- `1 <= numberOfBoxesi, numberOfUnitsPerBoxi <= 1000`
- `1 <= truckSize <= 106`

#### [937. 重新排列日志文件](https://leetcode-cn.com/problems/reorder-data-in-log-files/)

难度简单185

给你一个日志数组 `logs`。每条日志都是以空格分隔的字串，其第一个字为字母与数字混合的 **标识符** 。

有两种不同类型的日志：

- **字母日志**：除标识符之外，所有字均由小写字母组成
- **数字日志**：除标识符之外，所有字均由数字组成

请按下述规则将日志重新排序：

- 所有 **字母日志** 都排在 **数字日志** 之前。
- **字母日志** 在内容不同时，忽略标识符后，按内容字母顺序排序；在内容相同时，按标识符排序。
- **数字日志** 应该保留原来的相对顺序。

返回日志的最终顺序。

 

**示例 1：**

```
输入：logs = ["dig1 8 1 5 1","let1 art can","dig2 3 6","let2 own kit dig","let3 art zero"]
输出：["let1 art can","let3 art zero","let2 own kit dig","dig1 8 1 5 1","dig2 3 6"]
解释：
字母日志的内容都不同，所以顺序为 "art can", "art zero", "own kit dig" 。
数字日志保留原来的相对顺序 "dig1 8 1 5 1", "dig2 3 6" 。
```

**示例 2：**

```
输入：logs = ["a1 9 2 3 1","g1 act car","zo4 4 7","ab1 off key dog","a8 act zoo"]
输出：["g1 act car","a8 act zoo","ab1 off key dog","a1 9 2 3 1","zo4 4 7"]
```

 

**提示：**

- `1 <= logs.length <= 100`
- `3 <= logs[i].length <= 100`
- `logs[i]` 中，字与字之间都用 **单个** 空格分隔
- 题目数据保证 `logs[i]` 都有一个标识符，并且在标识符之后至少存在一个字

#### [20. 有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

难度简单3231

给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串 `s` ，判断字符串是否有效。

有效字符串需满足：

1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。

 

**示例 1：**

```
输入：s = "()"
输出：true
```

**示例 2：**

```
输入：s = "()[]{}"
输出：true
```

**示例 3：**

```
输入：s = "(]"
输出：false
```

**示例 4：**

```
输入：s = "([)]"
输出：false
```

**示例 5：**

```
输入：s = "{[]}"
输出：true
```

 

**提示：**

- `1 <= s.length <= 104`
- `s` 仅由括号 `'()[]{}'` 组成

#### [290. 单词规律](https://leetcode-cn.com/problems/word-pattern/)

难度简单465

给定一种规律 `pattern` 和一个字符串 `s` ，判断 `s` 是否遵循相同的规律。

这里的 **遵循** 指完全匹配，例如， `pattern` 里的每个字母和字符串 `str` 中的每个非空单词之间存在着双向连接的对应规律。

 

**示例1:**

```
输入: pattern = "abba", str = "dog cat cat dog"
输出: true
```

**示例 2:**

```
输入:pattern = "abba", str = "dog cat cat fish"
输出: false
```

**示例 3:**

```
输入: pattern = "aaaa", str = "dog cat cat dog"
输出: false
```

 

**提示:**

- `1 <= pattern.length <= 300`
- `pattern` 只包含小写英文字母
- `1 <= s.length <= 3000`
- `s` 只包含小写英文字母和 `' '`
- `s` **不包含** 任何前导或尾随对空格
- `s` 中每个单词都被 **单个空格** 分隔