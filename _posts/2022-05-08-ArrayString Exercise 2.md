---
layout:     post
title:      Array/String Exercise 2
subtitle:   
date:       2022-05-08
author:     Ethan
header-img: img/9.jpg
catalog: true
tags:
    - Leetcode
    - String

---
## Array/String Exercise 2

#### **(计算贡献828-2104)**



#### [828. 统计子串中的唯一字符](https://leetcode-cn.com/problems/count-unique-characters-of-all-substrings-of-a-given-string/)

难度困难109

我们定义了一个函数 `countUniqueChars(s)` 来统计字符串 `s` 中的唯一字符，并返回唯一字符的个数。

例如：`s = "LEETCODE"` ，则其中 `"L"`, `"T"`,`"C"`,`"O"`,`"D"` 都是唯一字符，因为它们只出现一次，所以 `countUniqueChars(s) = 5` 。

本题将会给你一个字符串 `s` ，我们需要返回 `countUniqueChars(t)` 的总和，其中 `t` 是 `s` 的子字符串。注意，某些子字符串可能是重复的，但你统计时也必须算上这些重复的子字符串（也就是说，你必须统计 `s` 的所有子字符串中的唯一字符）。

**由于答案可能非常大，请将结果 mod 10 ^ 9 + 7 后再返回。**

 

**示例 1：**

```
输入: s = "ABC"
输出: 10
解释: 所有可能的子串为："A","B","C","AB","BC" 和 "ABC"。
     其中，每一个子串都由独特字符构成。
     所以其长度总和为：1 + 1 + 1 + 2 + 2 + 3 = 10
```

**示例 2：**

```
输入: s = "ABA"
输出: 8
解释: 除了 countUniqueChars("ABA") = 1 之外，其余与示例 1 相同。
```

**示例 3：**

```
输入：s = "LEETCODE"
输出：92
```

 

**提示：**

- `0 <= s.length <= 10^5`
- `s` 只包含大写英文字符

思路：

- 想法是找到这个s中的所有字母，然后对于每个字母计算他单独出现的次数。因为求的是所有子串的单独出现的字母的次数的和，所以只要知道每个字母会单独出现多少次，所有字母次数加起来就是答案
- 比如对于 xXXAXXAXXAX，我们计算A单独出现的次数，我们首先要找到所有的A，然后看怎么让他们单独出现，不和其他A一起出现,假设A是在所以3，6，9出现
  - 第一个A的可能选择是（6-3）*（3-（-1））
  - 对于第二个A是（9-6）*（6-3）
  - 第三个是（len-9）*（9-6）
- "XAXAXXAX“ 对于它的第二个A，是index的（3-1）*（6-3）=6
  - For step 1 we have `"A(XA"` and `"AX(A"`, 2 possibility.
    For step 2 we have `"A)XXA"`, `"AX)XA"` and `"AXX)A"`, 3 possibilities
- 这道题可以用dict存所有index，会是O(N).但是前后只看三个位置，所以只要存最后两个，理论上是O(1)的空间
- `index[26][2]`记录每个大写字符的最后两个出现索引。
- 如果不是用ascii_uppercase，而是用字母索引，则是用ord()

代码：

![image-20220505124500642](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220505124500642.png)

#### [2262. 字符串的总引力](https://leetcode-cn.com/problems/total-appeal-of-a-string/)

难度困难47

字符串的 **引力** 定义为：字符串中 **不同** 字符的数量。

- 例如，`"abbca"` 的引力为 `3` ，因为其中有 `3` 个不同字符 `'a'`、`'b'` 和 `'c'` 。

给你一个字符串 `s` ，返回 **其所有子字符串的总引力** **。**

**子字符串** 定义为：字符串中的一个连续字符序列。

 

**示例 1：**

```
输入：s = "abbca"
输出：28
解释："abbca" 的子字符串有：
- 长度为 1 的子字符串："a"、"b"、"b"、"c"、"a" 的引力分别为 1、1、1、1、1，总和为 5 。
- 长度为 2 的子字符串："ab"、"bb"、"bc"、"ca" 的引力分别为 2、1、2、2 ，总和为 7 。
- 长度为 3 的子字符串："abb"、"bbc"、"bca" 的引力分别为 2、2、3 ，总和为 7 。
- 长度为 4 的子字符串："abbc"、"bbca" 的引力分别为 3、3 ，总和为 6 。
- 长度为 5 的子字符串："abbca" 的引力为 3 ，总和为 3 。
引力总和为 5 + 7 + 7 + 6 + 3 = 28 。
```

**示例 2：**

```
输入：s = "code"
输出：20
解释："code" 的子字符串有：
- 长度为 1 的子字符串："c"、"o"、"d"、"e" 的引力分别为 1、1、1、1 ，总和为 4 。
- 长度为 2 的子字符串："co"、"od"、"de" 的引力分别为 2、2、2 ，总和为 6 。
- 长度为 3 的子字符串："cod"、"ode" 的引力分别为 3、3 ，总和为 6 。
- 长度为 4 的子字符串："code" 的引力为 4 ，总和为 4 。
引力总和为 4 + 6 + 6 + 4 = 20 。
```

 

**提示：**

- `1 <= s.length <= 105`
- `s` 由小写英文字母组成

思路：

- 和上一题不同的点在于abb是2，之前会是1；bb是1，之前会是0

- ![image-20220505131446922](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220505131446922.png)

- ![image-20220505131621695](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220505131621695.png)

- assume we have string xxxaxxxxb..., with s[i] = a and s[j] = b.
  `s[i]` is th last character `a` before that `b`.

  对于以b结尾，我们需要算有多少个包含a的，如果需要包含a很简单，我们只要记住最后一个a的出现，那么这个a前面的任意位置作为开头都一定包含a

  We want to count, how many substring ending at `s[j]` contains character `a`.
  They are xxxaxxxxb, xxaxxxxb, xaxxxxb, axxxxb ....,
  `i + 1` substring ending with character `a` at `s[i]`,
  so we do `res += i + 1`.

  

  We repeatly do this for every `s[i]` and every one of 26 characters.

- ![image-20220505151338680](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220505151338680.png)

- ![image-20220505131700479](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220505131700479.png)

#### [907. 子数组的最小值之和](https://leetcode-cn.com/problems/sum-of-subarray-minimums/)

难度中等340

给定一个整数数组 `arr`，找到 `min(b)` 的总和，其中 `b` 的范围为 `arr` 的每个（连续）子数组。

由于答案可能很大，因此 **返回答案模 `10^9 + 7`** 。

 

**示例 1：**

```
输入：arr = [3,1,2,4]
输出：17
解释：
子数组为 [3]，[1]，[2]，[4]，[3,1]，[1,2]，[2,4]，[3,1,2]，[1,2,4]，[3,1,2,4]。 
最小值为 3，1，2，4，1，1，2，1，1，1，和为 17。
```

**示例 2：**

```
输入：arr = [11,81,94,43,3]
输出：444
```

 

**提示：**

- `1 <= arr.length <= 3 * 104`
- `1 <= arr[i] <= 3 * 104`



思路：

- 给定输入序列`A=[3,1,2,5,4]`，我们可以循环遍历数组并写出所有 以第 i 个元素**结尾的子数组。**

  ```
  [3]
  [3,1], [1]
  [3,1,2], [1,2], [2]
  [3,1,2,5], [1,2,5], [2,5], [5]
  [3,1,2,5,4], [1,2,5,4], [2,5,4], [5,4], [4]
  ```

- 我们可以用`result[i]`这些子数组的最小值之和来表示（以第 i 个元素结尾）。他们是这样的：

  ```
  3
  1 + 1
  1 + 1 + 2
  1 + 1 + 2 + 5
  1 + 1 + 2 + 4 + 4
  result = [3,2,4,9,12]
  ```

- 如果`A[i-1] <= A[i]`那时`result[i] = result[i-1] + A[i]`

  - A[i-1] = 1, A[i] = 2, result[i-1] = 2, result[i] = 4
  - A[i-1] = 2, A[i] = 5, result[i-1] = 4, result[i] = 5 

- 这是因为以第 i 个值结尾的子数组与第 (i-1) 个值的子数组基本相同，只是以A[i-1]结尾的后面加上了A[i], 然后多了一个单独的A[i]。由于A[i-1] <= A[i], 所以前面几个是不会受影响的，只有最后一个会受到影响

- 事实上，只要A[j] <= A[i], 并且j < i, 就可以得到result[i] = result[j] + A[i]*(i-j)

  - Let's take `i=4` and look at subarrays for the element `A[i]=4`，[3,1,2,5,4], [1,2,5,4], [2,5,4], [5,4], [4]
  - `j=2` as if we took those subarrays (`[3,1,2], [1,2], [2]`)， added elements `[5,4]` to each of them. Sum of those subarrays equals `result[j]`.

- 所以如果我们构建了一个非递减的堆栈，就可以找到前一个小于等于它的

- we add zeros to A and stack to avoid dealing with empty stack

代码：

![image-20220505162014566](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220505162014566.png)

#### [1498. 满足条件的子序列数目](https://leetcode-cn.com/problems/number-of-subsequences-that-satisfy-the-given-sum-condition/)

难度中等87

给你一个整数数组 `nums` 和一个整数 `target` 。

请你统计并返回 `nums` 中能满足其最小元素与最大元素的 **和** 小于或等于 `target` 的 **非空** 子序列的数目。

由于答案可能很大，请将结果对 `109 + 7` 取余后返回。

 

**示例 1：**

```
输入：nums = [3,5,6,7], target = 9
输出：4
解释：有 4 个子序列满足该条件。
[3] -> 最小元素 + 最大元素 <= target (3 + 3 <= 9)
[3,5] -> (3 + 5 <= 9)
[3,5,6] -> (3 + 6 <= 9)
[3,6] -> (3 + 6 <= 9)
```

**示例 2：**

```
输入：nums = [3,3,6,8], target = 10
输出：6
解释：有 6 个子序列满足该条件。（nums 中可以有重复数字）
[3] , [3] , [3,3], [3,6] , [3,6] , [3,3,6]
```

**示例 3：**

```
输入：nums = [2,3,3,4,6,7], target = 12
输出：61
解释：共有 63 个非空子序列，其中 2 个不满足条件（[6,7], [7]）
有效序列总数为（63 - 2 = 61）
```

 

**提示：**

- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 106`
- `1 <= target <= 106`

#### [2104. 子数组范围和](https://leetcode-cn.com/problems/sum-of-subarray-ranges/)

难度中等191

给你一个整数数组 `nums` 。`nums` 中，子数组的 **范围** 是子数组中最大元素和最小元素的差值。

返回 `nums` 中 **所有** 子数组范围的 **和** *。*

子数组是数组中一个连续 **非空** 的元素序列。

 

**示例 1：**

```
输入：nums = [1,2,3]
输出：4
解释：nums 的 6 个子数组如下所示：
[1]，范围 = 最大 - 最小 = 1 - 1 = 0 
[2]，范围 = 2 - 2 = 0
[3]，范围 = 3 - 3 = 0
[1,2]，范围 = 2 - 1 = 1
[2,3]，范围 = 3 - 2 = 1
[1,2,3]，范围 = 3 - 1 = 2
所有范围的和是 0 + 0 + 0 + 1 + 1 + 2 = 4
```

**示例 2：**

```
输入：nums = [1,3,3]
输出：4
解释：nums 的 6 个子数组如下所示：
[1]，范围 = 最大 - 最小 = 1 - 1 = 0
[3]，范围 = 3 - 3 = 0
[3]，范围 = 3 - 3 = 0
[1,3]，范围 = 3 - 1 = 2
[3,3]，范围 = 3 - 3 = 0
[1,3,3]，范围 = 3 - 1 = 2
所有范围的和是 0 + 0 + 0 + 2 + 0 + 2 = 4
```

**示例 3：**

```
输入：nums = [4,-2,-3,4,1]
输出：59
解释：nums 中所有子数组范围的和是 59
```

 

**提示：**

- `1 <= nums.length <= 1000`
- `-109 <= nums[i] <= 109`

 

**进阶：**你可以设计一种时间复杂度为 `O(n)` 的解决方案吗？



#### [65. 有效数字](https://leetcode-cn.com/problems/valid-number/)

难度困难310

**有效数字**（按顺序）可以分成以下几个部分：

1. 一个 **小数** 或者 **整数**
2. （可选）一个 `'e'` 或 `'E'` ，后面跟着一个 **整数**

**小数**（按顺序）可以分成以下几个部分：

1. （可选）一个符号字符（`'+'` 或 `'-'`）
2. 下述格式之一：
   1. 至少一位数字，后面跟着一个点 `'.'`
   2. 至少一位数字，后面跟着一个点 `'.'` ，后面再跟着至少一位数字
   3. 一个点 `'.'` ，后面跟着至少一位数字

**整数**（按顺序）可以分成以下几个部分：

1. （可选）一个符号字符（`'+'` 或 `'-'`）
2. 至少一位数字

部分有效数字列举如下：`["2", "0089", "-0.1", "+3.14", "4.", "-.9", "2e10", "-90E3", "3e+7", "+6e-1", "53.5e93", "-123.456e789"]`

部分无效数字列举如下：`["abc", "1a", "1e", "e3", "99e2.5", "--6", "-+3", "95a54e53"]`

给你一个字符串 `s` ，如果 `s` 是一个 **有效数字** ，请返回 `true` 。

 

**示例 1：**

```
输入：s = "0"
输出：true
```

**示例 2：**

```
输入：s = "e"
输出：false
```

**示例 3：**

```
输入：s = "."
输出：false
```

 

**提示：**

- `1 <= s.length <= 20`
- `s` 仅含英文字母（大写和小写），数字（`0-9`），加号 `'+'` ，减号 `'-'` ，或者点 `'.'` 。

思路：

- this is not your typical LeetCode problem, but a problem that is highly representative of a "real world" problem - a seemingly simple task that is frustratingly full of edge cases.
- **Interview Tip:** Asked a question like this in an interview? Be sure to communicate thoroughly with your interviewer to make sure you're covering all cases.
- 如果到目前为止它可以认为是数字，就让seen_digit为True，如果碰到e，就要设置他为false
  - At the end, return `seenDigit`. This is one reason why we have to reset `seenDigit` after seeing an exponent - otherwise an input like `"21e"` would be incorrectly judged as valid.
  - 但也需要注意，dot不需要前面有digit，也不需要后面有，比如4.也是ok的

代码：

![image-20220504120110179](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504120110179.png)

- 时间复杂度是O(N)
- 空间复杂度是O(1)

#### [76. 最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/)

难度困难1614

给你一个字符串 `s` 、一个字符串 `t` 。返回 `s` 中涵盖 `t` 所有字符的最小子串。如果 `s` 中不存在涵盖 `t` 所有字符的子串，则返回空字符串 `""` 。

 

**注意：**

- 对于 `t` 中重复字符，我们寻找的子字符串中该字符数量必须不少于 `t` 中该字符数量。
- 如果 `s` 中存在这样的子串，我们保证它是唯一的答案。

 

**示例 1：**

```
输入：s = "ADOBECODEBANC", t = "ABC"
输出："BANC"
```

**示例 2：**

```
输入：s = "a", t = "a"
输出："a"
```

**示例 3:**

```
输入: s = "a", t = "aa"
输出: ""
解释: t 中两个字符 'a' 均应包含在 s 的子串中，
因此没有符合条件的子字符串，返回空字符串。
```

思路：



代码：

#### [28. Implement strStr()](https://leetcode-cn.com/problems/implement-strstr/)

难度简单1414

Implement [strStr()](http://www.cplusplus.com/reference/cstring/strstr/).

Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

**Clarification:**

What should we return when `needle` is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C's [strstr()](http://www.cplusplus.com/reference/cstring/strstr/) and Java's [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)).

 

**Example 1:**

```
Input: haystack = "hello", needle = "ll"
Output: 2
```

**Example 2:**

```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

 

**Constraints:**

- `1 <= haystack.length, needle.length <= 104`
- `haystack` and `needle` consist of only lowercase English characters.