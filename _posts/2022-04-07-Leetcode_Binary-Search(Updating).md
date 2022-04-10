---
layout:     post
title:      Binary Search(Updating)
subtitle:   
date:       2022-04-07
author:     Ethan
header-img: img/2.jpg
catalog: true
tags:
    - Leetcode
    - Binary Search
---

> 二分查找中使用的术语：
>
> 目标 Target —— 你要查找的值
> 索引 Index —— 你要查找的当前位置
> 左、右指示符 Left，Right —— 我们用来维持查找空间的指标
> 中间指示符 Mid —— 我们用来应用条件来确定我们应该向左查找还是向右查找的索引

> 时间：O(log n) —— 算法时间
>
> 因为二分查找是通过对查找空间中间的值应用一个条件来操作的，并因此将查找空间折半，在更糟糕的情况下，我们将不得不进行 O(log n) 次比较，其中 n 是集合中元素的数目。
>
> 为什么是 log n？
>
> 二分查找是通过将现有数组一分为二来执行的。
> 因此，每次调用子例程(或完成一次迭代)时，其大小都会减少到现有部分的一半。
> 首先 N 变成 N/2，然后又变成 N/4，然后继续下去，直到找到元素或尺寸变为 1。
> 迭代的最大次数是 log N (base 2) 。

感觉最难的就在于while的left是小于等于还是小于right

#### 二分查找模板

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220407102616860.png" alt="image-20220407102616860" style="zoom:50%;" />

搜索区间是 [left, mid - 1] 或者 [mid + 1, right] 

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220407111311017.png" alt="image-20220407111311017" style="zoom:50%;" />

搜索左侧边界

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/1566782-20190624225555183-2085599880.jpg)

「搜索区间」是 [left, right) 左闭右开，所以当 nums[mid] 被检测之后，下一步的搜索区间应该去掉 mid 分割成两个区间，即 [left, mid) 或 [mid + 1, right)。

![image-20220407124004726](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220407124004726.png)

![image-20220407115920934](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220407115920934.png)

#### [278. 第一个错误的版本](https://leetcode-cn.com/problems/first-bad-version/)

难度简单650

你是产品经理，目前正在带领一个团队开发新的产品。不幸的是，你的产品的最新版本没有通过质量检测。由于每个版本都是基于之前的版本开发的，所以错误的版本之后的所有版本都是错的。

假设你有 `n` 个版本 `[1, 2, ..., n]`，你想找出导致之后所有版本出错的第一个错误的版本。

你可以通过调用 `bool isBadVersion(version)` 接口来判断版本号 `version` 是否在单元测试中出错。实现一个函数来查找第一个错误的版本。你应该尽量减少对调用 API 的次数。

**示例 1：**

```
输入：n = 5, bad = 4
输出：4
解释：
调用 isBadVersion(3) -> false 
调用 isBadVersion(5) -> true 
调用 isBadVersion(4) -> true
所以，4 是第一个错误的版本。
```

**示例 2：**

```
输入：n = 1, bad = 1
输出：1
```

思路：

- 注意这里的是从1开始的，所以定义left和right时要注意
- 我们要找到的是版本是正好左边是好的，右边是坏的
- 每次我们都找到其中间的版本，检查其是否为正确版本。
  - 如果为正确版本，那么第一个错误的版本必然位于该版本的右侧；
  - 否则第一个错误的版本必然位于该版本及该版本的左侧，我们缩紧右边界。
- 注意我们希望API调用的越少越好，所以不可以在知道right是badversion后在对right+1和right-1检测，这样的风险太高

代码：

![image-20220407112412890](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220407112412890.png)

#### [162. 寻找峰值](https://leetcode-cn.com/problems/find-peak-element/)

难度中等775

峰值元素是指其值严格大于左右相邻值的元素。

给你一个整数数组 `nums`，找到峰值元素并返回其索引。数组可能包含多个峰值，在这种情况下，返回 **任何一个峰值** 所在位置即可。

你可以假设 `nums[-1] = nums[n] = -∞` 。

你必须实现时间复杂度为 `O(log n)` 的算法来解决此问题。

 

**示例 1：**

```
输入：nums = [1,2,3,1]
输出：2
解释：3 是峰值元素，你的函数应该返回其索引 2。
```

**示例 2：**

```
输入：nums = [1,2,1,3,5,6,4]
输出：1 或 5 
解释：你的函数可以返回索引 1，其峰值元素为 2；
     或者返回索引 5， 其峰值元素为 6。
```

思路：

看到O(lgn)，首先想到的就是二分查找

但是先想想其他的

- 看到说峰值严格比其他大，其实就遍历一遍数组，找到最大的，然后保存index就好了。但是这样的复杂度为O(n)
- 提到峰值，就想让 nums[i] 跟 nums[i-1], nums[i+1] 都比较一下，但其实只需要找出是单调递增还是单调递减就行了。
- 如果递增，nums[mid] < nums[mid+1], 那么峰值一定在mid的右边，left = mid+1
  - 让我困惑的是为什么left要加一，但是不加一，确实有问题，left和right最后缩不到一起

代码：

- 在常规的二分模板中，直接使用 right = len(nums), right 遍历过程中是取不到 len(nums)这个值的
- 而在这里再减去 1，主要是为了避免 nums[mid+1] 数组越界，而且又不妨碍最终的答案落在 len(nums) - 1 上

![image-20220407120718277](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220407120718277.png)

#### [153. 寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

难度中等716

已知一个长度为 `n` 的数组，预先按照升序排列，经由 `1` 到 `n` 次 **旋转** 后，得到输入数组。例如，原数组 `nums = [0,1,2,4,5,6,7]` 在变化后可能得到：

- 若旋转 `4` 次，则可以得到 `[4,5,6,7,0,1,2]`
- 若旋转 `7` 次，则可以得到 `[0,1,2,4,5,6,7]`

注意，数组 `[a[0], a[1], a[2], ..., a[n-1]]` **旋转一次** 的结果为数组 `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]` 。

给你一个元素值 **互不相同** 的数组 `nums` ，它原来是一个升序排列的数组，并按上述情形进行了多次旋转。请你找出并返回数组中的 **最小元素** 。

你必须设计一个时间复杂度为 `O(log n)` 的算法解决此问题。

 

**示例 1：**

```
输入：nums = [3,4,5,1,2]
输出：1
解释：原数组为 [1,2,3,4,5] ，旋转 3 次得到输入数组。
```

**示例 2：**

```
输入：nums = [4,5,6,7,0,1,2]
输出：0
解释：原数组为 [0,1,2,4,5,6,7] ，旋转 4 次得到输入数组。
```

**示例 3：**

```
输入：nums = [11,13,15,17]
输出：11
解释：原数组为 [11,13,15,17] ，旋转 4 次得到输入数组。
```

 

#### [剑指 Offer 11. 旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/) &[154. 寻找旋转排序数组中的最小值 II](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)

难度简单593

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。

给你一个可能存在 **重复** 元素值的数组 `numbers` ，它原来是一个升序排列的数组，并按上述情形进行了一次旋转。请返回旋转数组的**最小元素**。例如，数组 `[3,4,5,1,2]` 为 `[1,2,3,4,5]` 的一次旋转，该数组的最小值为 1。 

注意，数组 `[a[0], a[1], a[2], ..., a[n-1]]` 旋转一次 的结果为数组 `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]` 。

 

**示例 1：**

```
输入：numbers = [3,4,5,1,2]
输出：1
```

**示例 2：**

```
输入：numbers = [2,2,2,0,1]
输出：0
```