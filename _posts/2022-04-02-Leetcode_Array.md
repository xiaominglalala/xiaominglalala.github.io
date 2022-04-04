---
layout:     post
title:      Array
subtitle:   
date:       2022-04-2
author:     Ethan
header-img: img/10.jpg
catalog: true
tags:
    - Leetcode
    - Array
---

## 数组

#### [704. 二分查找](https://leetcode-cn.com/problems/binary-search/)

难度简单586收藏分享切换为英文接收动态反馈

给定一个 `n` 个元素有序的（升序）整型数组 `nums` 和一个目标值 `target` ，写一个函数搜索 `nums` 中的 `target`，如果目标值存在返回下标，否则返回 `-1`。


**示例 1:**

```
输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4
```

**示例 2:**

```
输入: nums = [-1,0,3,5,9,12], target = 2
输出: -1
解释: 2 不存在 nums 中因此返回 -1
```

思路：

- 对于有序数组+数组中无重复元素，可以考虑使用二分查找
- 对于二分查找，主要需要注意两种情况
  - 首先是右边是闭合的
    - 如果右边是闭合的，在写while循环时，就需要使用<=  `while (left <= right)` 
    - 并且对于第二次查找，下标将会是middle + 1或者middle - 1
    - 范围从0到 len(nums)
  - 其次是右边是开的
    - 如果右边是开的，在写while循环时，就需要使用<`while (left < right)`
    - 次时对于第二次查找，就需要把middle加入考虑；middle或者middle+1
    - 范围从0到 len(nums-1)
- middle = (left + right) // 2 使用整除

代码：

![image-20220202164310357](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220202164310357.png)

or

![image-20220202164552584](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220202164552584.png)

#### [27. 移除元素](https://leetcode-cn.com/problems/remove-element/)

难度简单1149

给你一个数组 `nums` 和一个值 `val`，你需要 **[原地](https://baike.baidu.com/item/原地算法)** 移除所有数值等于 `val` 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 `O(1)` 额外空间并 **[原地 ](https://baike.baidu.com/item/原地算法)修改输入数组**。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

 

**说明:**

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以**「引用」**方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

```
// nums 是以“引用”方式传递的。也就是说，不对实参作任何拷贝
int len = removeElement(nums, val);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

 

**示例 1：**

```
输入：nums = [3,2,2,3], val = 3
输出：2, nums = [2,2]
解释：函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。你不需要考虑数组中超出新长度后面的元素。例如，函数返回的新长度为 2 ，而 nums = [2,2,3,3] 或 nums = [2,2,0,0]，也会被视作正确答案。
```

**示例 2：**

```
输入：nums = [0,1,2,2,3,0,4,2], val = 2
输出：5, nums = [0,1,4,0,3]
解释：函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。注意这五个元素可为任意顺序。你不需要考虑数组中超出新长度后面的元素。
```

思路：

- 暴力法：

  ![27.移除元素-暴力解法](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/008eGmZEly1gntrc7x9tjg30du09m1ky.gif)

- 双指针法：

  ![27.移除元素-双指针法](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/008eGmZEly1gntrds6r59g30du09mnpd.gif)

- fast指针每次while循环都会向前。而slow指针只会在fast指针指的不是要删除元素时才会向前

- 每次slow指针要动时，会和fast指针交换信息

- 注意最后要return slow来确定长度

代码：

![image-20220202172712071](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220202172712071.png)

#### [977. 有序数组的平方](https://leetcode-cn.com/problems/squares-of-a-sorted-array/)

难度简单405

给你一个按 **非递减顺序** 排序的整数数组 `nums`，返回 **每个数字的平方** 组成的新数组，要求也按 **非递减顺序** 排序。



 

**示例 1：**

```
输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]
解释：平方后，数组变为 [16,1,0,9,100]
排序后，数组变为 [0,1,9,16,100]
```

**示例 2：**

```
输入：nums = [-7,-3,2,3,11]
输出：[4,9,9,49,121]
```

思路：

- 如果使用暴力法，也就是全部平方后再排序，会是O(n\log n)的复杂度
- 这道题使用双指针法：
  - 首先一个指针指向尾部，一个指向头部
  - 显然最大的平方数要么就是在尾部，要么就是头部
  - 那么两者比较，谁大，谁就放在result最后面
- ![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/977.%25E6%259C%2589%25E5%25BA%258F%25E6%2595%25B0%25E7%25BB%2584%25E7%259A%2584%25E5%25B9%25B3%25E6%2596%25B9.gif)

代码：

![image-20220203134056583](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220203134056583.png)

#### [209. 长度最小的子数组](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)

难度中等894

给定一个含有 `n` 个正整数的数组和一个正整数 `target` **。**

找出该数组中满足其和 `≥ target` 的长度最小的 **连续子数组** `[numsl, numsl+1, ..., numsr-1, numsr]` ，并返回其长度**。**如果不存在符合条件的子数组，返回 `0` 。

 

**示例 1：**

```
输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。
```

**示例 2：**

```
输入：target = 4, nums = [1,4,4]
输出：1
```

**示例 3：**

```
输入：target = 11, nums = [1,1,1,1,1,1,1,1]
输出：0
```

思路：

- 如果使用暴力法，相当于是两个for循环是O(n^2)
- 这里使用滑动窗口，类似于双指针。存储一个变量result来保存当前见过最小的长度
- ![209.长度最小的子数组](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/209.%25E9%2595%25BF%25E5%25BA%25A6%25E6%259C%2580%25E5%25B0%258F%25E7%259A%2584%25E5%25AD%2590%25E6%2595%25B0%25E7%25BB%2584.gif)
- 首先初始化result为一个不可能存在的较大的结果，比如`len(nums)+1`，最后检验result如果仍然是这个值，返回0，说明没有这样的字串

代码：

![image-20220203160650431](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220203160650431.png)



#### [59. 螺旋矩阵 II](https://leetcode-cn.com/problems/spiral-matrix-ii/)

难度中等574

给你一个正整数 `n` ，生成一个包含 `1` 到 `n2` 所有元素，且元素按顺时针顺序螺旋排列的 `n x n` 正方形矩阵 `matrix` 。

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/spiraln.jpg)

```
输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]
```

**示例 2：**

```
输入：n = 1
输出：[[1]]
```

思路：

- 遵循左闭右开的原则，在拐弯处让给新的一条边
- ![螺旋矩阵](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/2020121623550681.png)
- 首先是初始化矩阵，比如输入3，我们初始化是[[0,0,0],[0,0,0],[0,0,0]]。也就是[[0]*n for i in range(n)]
  - ![image-20220203162351757](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220203162351757.png)
  - ![image-20220203162406298](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220203162406298.png)
- 其次是确定边界
  - 初始：left = 0; right = n - 1; up = 0; down = n - 1
  - 其中从下往上和从右往左这种倒序的表达方式：![image-20220203202955580](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220203202955580.png)
  - 迭代一轮后，left += 1; right -= 1 up += 1 down -= 1
- 然后是循环的终止条件，是up <down 并且 left < right，而不是相等，因为偶的情况将直接超过那个位置
- 最后是确定特殊情况，如果n是偶数，就是一直转圈，不用到中心。如果n是奇数，需要判断
  - 首先是奇数的判断方法：`n%2`

代码：

![image-20220203203958816](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220203203958816.png)

![image-20220203204019607](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220203204019607.png)





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

#### [162. Find Peak Element](https://leetcode-cn.com/problems/find-peak-element/)

难度中等770

A peak element is an element that is strictly greater than its neighbors.

Given an integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You may imagine that `nums[-1] = nums[n] = -∞`.

You must write an algorithm that runs in `O(log n)` time.

 

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

**Example 2:**

```
Input: nums = [1,2,1,3,5,6,4]
Output: 5
Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.
```