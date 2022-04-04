---
layout:     post
title:      Dynamic Programming
subtitle:   
date:       2022-03-30
author:     Ethan
header-img: img/5.jpg
catalog: true
tags:
    - Leetcode
    - Dynamic Programming
---

# 动态规划

- 动态规划和贪心的区别？
  - 贪心没有状态推导，而是从局部直接选最优的
  - 动态规划中每一个状态一定是由上一个状态推导出来的
- **对于动态规划问题五步曲**
  1. 确定dp数组（dp table）以及下标的含义
  2. 确定递推公式
  3. dp数组如何初始化
  4. 确定遍历顺序
  5. 举例推导dp数组

## 1. 基础题目

#### [509. 斐波那契数](https://leetcode-cn.com/problems/fibonacci-number/)

难度简单405收藏分享切换为英文接收动态反馈

**斐波那契数** （通常用 `F(n)` 表示）形成的序列称为 **斐波那契数列** 。该数列由 `0` 和 `1` 开始，后面的每一项数字都是前面两项数字的和。也就是：

```
F(0) = 0，F(1) = 1
F(n) = F(n - 1) + F(n - 2)，其中 n > 1
```

给定 `n` ，请计算 `F(n)` 。

 

**示例 1：**

```
输入：n = 2
输出：1
解释：F(2) = F(1) + F(0) = 1 + 0 = 1
```

**示例 2：**

```
输入：n = 3
输出：2
解释：F(3) = F(2) + F(1) = 1 + 1 = 2
```

**示例 3：**

```
输入：n = 4
输出：3
解释：F(4) = F(3) + F(2) = 2 + 1 = 3
```

思路：

- 第一步，确定dp数组的意义：dp[i]代表第i个斐波那契数的值
- 第二步，确定递推公式：dp[i] = dp[i-1]+dp[i-2]
- 第三步，dp数组初始化：dp[0] = 0, dp[1] = 1
- 第四步， 确定遍历顺序：从前往后
- 第五步，举例子来验证

代码：



#### [70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

难度简单2221收藏分享切换为英文接收动态反馈

假设你正在爬楼梯。需要 `n` 阶你才能到达楼顶。

每次你可以爬 `1` 或 `2` 个台阶。你有多少种不同的方法可以爬到楼顶呢？

 

**示例 1：**

```
输入：n = 2
输出：2
解释：有两种方法可以爬到楼顶。
1. 1 阶 + 1 阶
2. 2 阶
```

**示例 2：**

```
输入：n = 3
输出：3
解释：有三种方法可以爬到楼顶。
1. 1 阶 + 1 阶 + 1 阶
2. 1 阶 + 2 阶
3. 2 阶 + 1 阶
```

思路：

- 第一步，确定dp[i]的含义：i层楼有几种爬法
- 第二步，确定递推公式：dp[i] = dp[i-1] *1+dp[i-2] *1 
  - 到第i层，无非是在i-1层走了一步或者在i-2层走了两步
- 第三步确定初始化：dp[1] = 1, dp[2] = 2
- 第四步确定遍历顺序：从i-1和i-2推i，显然是从前往后
- 第五步：举例子

> 之后第四第五步可以不要了

代码：

![image-20220301220750008](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220301220750008.png)

时间和空间复杂度都是O(n), 有空间O(1)的方法

#### [746. 使用最小花费爬楼梯](https://leetcode-cn.com/problems/min-cost-climbing-stairs/)

难度简单814收藏分享切换为英文接收动态反馈

给你一个整数数组 `cost` ，其中 `cost[i]` 是从楼梯第 `i` 个台阶向上爬需要支付的费用。一旦你支付此费用，即可选择向上爬一个或者两个台阶。

你可以选择从下标为 `0` 或下标为 `1` 的台阶开始爬楼梯。

请你计算并返回达到楼梯顶部的最低花费。

 

**示例 1：**

```
输入：cost = [10,15,20]
输出：15
解释：你将从下标为 1 的台阶开始。
- 支付 15 ，向上爬两个台阶，到达楼梯顶部。
总花费为 15 。
```

**示例 2：**

```
输入：cost = [1,100,1,1,1,100,1,1,100,1]
输出：6
解释：你将从下标为 0 的台阶开始。
- 支付 1 ，向上爬两个台阶，到达下标为 2 的台阶。
- 支付 1 ，向上爬两个台阶，到达下标为 4 的台阶。
- 支付 1 ，向上爬两个台阶，到达下标为 6 的台阶。
- 支付 1 ，向上爬一个台阶，到达下标为 7 的台阶。
- 支付 1 ，向上爬两个台阶，到达下标为 9 的台阶。
- 支付 1 ，向上爬一个台阶，到达楼梯顶部。
总花费为 6 。
```

思路：

- dp[i] 是第i层的最低花费
- 因为是一定要走到底，所以不用纠结dp是n还是n-1，只要用和cost的长度和下标一样就行
- 默认每一步都要收费，但如果是最后一步，就不收费
  - 这是很重要的，就是决定了dp的递推公式是加`c[i]`, 而最后return的是dp[i-1]和dp[i-2]中小的那个

- 递推关系是什么？第i层的最低花费是min（第i层的花费加上前i-1的最低花费，第i层的花费加上前i-2的最低花费）。
  - `dp[i] = min(dp[i-1], dp[i-2]) +c[i]`
- 初始化：`dp[0] = c[0], dp[1] = c[1]`

代码：

![image-20220330225001498](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220330225001498.png)



#### [62. 不同路径](https://leetcode-cn.com/problems/unique-paths/)

难度中等1288收藏分享切换为英文接收动态反馈

一个机器人位于一个 `m x n` 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish” ）。

问总共有多少条不同的路径？

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/robot_maze.png)

```
输入：m = 3, n = 7
输出：28
```

**示例 2：**

```
输入：m = 3, n = 2
输出：3
解释：
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右
3. 向下 -> 向右 -> 向下
```

**示例 3：**

```
输入：m = 7, n = 3
输出：28
```

**示例 4：**

```
输入：m = 3, n = 3
输出：6
```

思路：

- 首先是dp[i,j]，到达i，j点有几种路径

- dp[i] [j]=dp[i-1] [j]+dp[i] [j-1]: 只可能是从上面或者下面来的

- ~~dp[0, 0] = 1~~整个dp都初始化为1

- 这里的初始化方法要注意（二阶的初始化）：里面的for是行，这样每一行都是一个长为n的list

  - 

- 注意把每个点的值初始化为一，这样每走一步都能加一次

- 时间和空间复杂度都是O（m*n）

  

代码：

可以一开始都当1，思路清晰的话，应该是边缘是1

![image-20220303113303814](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220303113303814.png)

![image-20220303143817107](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220303143817107.png)

#### [63. 不同路径 II](https://leetcode-cn.com/problems/unique-paths-ii/)

难度中等736收藏分享切换为英文接收动态反馈

一个机器人位于一个 `m x n` 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

网格中的障碍物和空位置分别用 `1` 和 `0` 来表示。

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/robot1.jpg)

```
输入：obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
输出：2
解释：3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右
```

**示例 2：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/robot2.jpg)

```
输入：obstacleGrid = [[0,1],[0,0]]
输出：1
```

思路：

- 相比上一道题，区别就是需要在遍历dp时，需要进行判断，只有没有障碍时，才能使用递推式
- 第一步，确定dp: dp[i] [j]代表从(0,0)到i，j的路线数目
- 第二步，确定递推式：加上障碍判断的dp[i] [j]=dp[i-1] [j]+dp[i] [j-1]，如果有障碍就保持原样，等迭代过掉这个点
- 第三步，初始化：不同于之前的全部为1，这里应该注意如果边缘的地方出现障碍，后面的位置都应该为0
  - <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20210104114513928.png" alt="63.不同路径II" style="zoom:50%;" />
  - 具体上要判断第一个（0，0）位置是不是障碍，是，直接返回0
  - 然后遍历整个dp的两边，赋值1，因为只写地方只有一种到达的方式
  - <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220303142846167.png" alt="image-20220303142846167" style="zoom:25%;" />
  - 其他的地方就是dp计算就好了

- 注意，这里给的没有长和宽，要自己提取，提取的方式是
  - 行数：![image-20220303121125370](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220303121125370.png)
  - 列数：![image-20220303121136606](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220303121136606.png)

代码：

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220303161319272.png" alt="image-20220303161319272" style="zoom: 67%;" />

#### [343. 整数拆分](https://leetcode-cn.com/problems/integer-break/)

难度中等722

给定一个正整数 `n` ，将其拆分为 `k` 个 **正整数** 的和（ `k >= 2` ），并使这些整数的乘积最大化。

返回 *你可以获得的最大乘积* 。

 

**示例 1:**

```
输入: n = 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1。
```

**示例 2:**

```
输入: n = 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

思路：

- dp[i]: 对于整数i的最大拆分
- 递推式：dp[i] = max{dp[i], dp[i-j] *j, (i-j) *j}
  - 其中j是从1遍历到i-1
  - dp[i-j] *j是对i-j进行计算最大拆分
  -  (i-j) *j是直接相乘
- 初始化：没必要考虑0和1，从dp[2] = 1开始

代码：

![image-20220303173441326](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220303173441326.png)

#### [96. 不同的二叉搜索树](https://leetcode-cn.com/problems/unique-binary-search-trees/)

难度中等1579收藏分享切换为英文接收动态反馈

给你一个整数 `n` ，求恰由 `n` 个节点组成且节点值从 `1` 到 `n` 互不相同的 **二叉搜索树** 有多少种？返回满足题意的二叉搜索树的种数。

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/uniquebstn3.jpg)

```
输入：n = 3
输出：5
```

**示例 2：**

```
输入：n = 1
输出：1
```

思路：

- 确定dp[i]的意义： **1到i为节点组成的二叉搜索树的个数为dp[i]**
- 先举个例子：<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20210107093129889.png" alt="96.不同的二叉搜索树1" style="zoom:50%;" />
  - 比如n = 3，我们考虑dp[3], 就是元素1为头结点搜索树的数量 + 元素2为头结点搜索树的数量 + 元素3为头结点搜索树的数量
  - 元素1为头结点搜索树的数量 = 右子树有2个元素的搜索树数量 * 左子树有0个元素的搜索树数量 = dp[2]*dp[0]
  - 元素2为头结点搜索树的数量 = 右子树有1个元素的搜索树数量 * 左子树有1个元素的搜索树数量 = dp[1]*dp[1]
  - 元素3为头结点搜索树的数量 = 右子树有0个元素的搜索树数量 * 左子树有2个元素的搜索树数量 = dp[0]*dp[2]

- dp[i] = sum(dp[j]*dp[i-j-1]), 其中j从0到i-1
- 初始化：dp[0] = 1, dp[1] = 1

代码：

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220303180310728.png" alt="image-20220303180310728" style="zoom: 67%;" />

## 2. 背包问题

### 2.1 01背包

- 有n件物品和一个最多能背重量为w 的背包。第i件物品的重量是weight[i]，得到的价值是value[i] 。**每件物品只能用一次**，求解将哪些物品装入背包里物品价值总和最大。

- 举一个例子：

  背包最大重量为4。

  物品为：

  |       | 重量 | 价值 |
  | ----- | ---- | ---- |
  | 物品0 | 1    | 15   |
  | 物品1 | 3    | 20   |
  | 物品2 | 4    | 30   |

  问背包能背的物品最大价值是多少？

- dp数组的意义：即**dp[i] [j] 表示从下标为[0-i]的物品里任意取，放进容量为j的背包，价值总和最大是多少**

- 递推式：

  - `dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i]);`
  - **放物品i**：`dp[i - 1][j - weight[i]]` 为背包容量为j - weight[i]的时候不放物品i的最大价值；`dp[i - 1][j - weight[i]] + value[i] `就是背包放物品i得到的最大价值
  - **不放物品i**：`dp[i - 1][j]`(其实就是当物品i的重量大于背包j的重量时，物品i无法放进背包中，所以被背包内的价值依然和前面相同。)

- 初始化：

  - 如果背包容量j为0，无论是选取哪些物品，背包价值总和一定为0：<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/2021011010304192.png" alt="动态规划-背包问题2" style="zoom:50%;" />
  - i为0，存放编号0的物品的时候， j < weight[0]的时候，dp[0] [j] 应该是 0；j >= weight[0]时，dp[0] [j] 应该是value[0]，因为背包容量放足够放编号0物品<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20210110103109140.png" alt="动态规划-背包问题7" style="zoom:50%;" />
  - 对于其他部分 统一把dp数组统一初始为0，更方便一些
  - 有两个遍历的维度：物品与背包重量；**但是先遍历物品更好理解**

如果使用**一维滚动数组**

> 状态压缩

- dp[j]表示：容量为j的背包，所背的物品价值可以最大为dp[j]

- dp[j]有两个选择，一个是取自己当前的dp[j] ，即不放物品i，一个是取dp[j - weight[i]] + value[i]，即放物品i。二者取最大

- ```python
  dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);
  ```

  dp[j - weight[i]]表示容量为j - weight[i]的背包所背的最大价值。

  dp[j - weight[i]] + value[i] 表示容量为j的背包，放入物品i了之后的价值

- dp数组初始化的时候，都初始为0

- 遍历顺序与二维时不同，是倒序遍历，**为了保证物品i只被放入一次！**

#### [416. Partition Equal Subset Sum](https://leetcode-cn.com/problems/partition-equal-subset-sum/)

难度中等1232收藏分享切换为中文接收动态反馈

Given a **non-empty** array `nums` containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

 

**Example 1:**

```
Input: nums = [1,5,11,5]
Output: true
Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

**Example 2:**

```
Input: nums = [1,2,3,5]
Output: false
Explanation: The array cannot be partitioned into equal sum subsets.
```

思路：

- **即一个商品如果可以重复多次放入是完全背包，而只能放入一次是01背包**

- 本题要求集合里能否出现总和为 sum / 2 的子集

- 动态规划五部曲

  - 确定dp数组以及下标的含义：**dp[j]表示 背包总容量是j，最大可以凑成j的子集总和为dp[j]**

  - 确定递推公式：01背包的递推公式为：dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);

    - dp[j - weight[i]]表示容量为j - weight[i]的背包所背的最大价值。
    - dp[j - weight[i]] + value[i] 表示容量为j的背包，放入物品i了之后的价值
    - 在这道题中，weight和value是等价的数值，所以是dp[j]=max(dp[j], dp[j-num[i]]+num[i])

  - 如何初始化dp数组：都初始为0

  - 确定遍历顺序：如果使用一维dp数组，物品遍历的for循环放在外层，遍历背包的for循环放在内层，且内层for循环倒序遍历！

    - ```cpp
      for(int i = 0; i < nums.size(); i++) {
          for(int j = target; j >= nums[i]; j--) { // 每一个元素一定是不可重复放入，所以从大到小遍历
              dp[j] = max(dp[j], dp[j - nums[i]] + nums[i]);
          }
      }
      ```

  - 举例推导dp数组：比如输入[1,5,11,5], 则target = (1+5+5+11)/2=11;我们希望看到dp[target] == target

- 对于i=0，对于容量为11~1的背包，最多存入1![image-20220402152153079](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220402152153079.png)

- 对于i=1，也就是对于容量为11~6的背包，将最多存入1+5=6![image-20220402152315779](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220402152315779.png)

- 对于i=2，也就是容量为11的背包，最多存入11，dp[11]会变成11![image-20220402152347950](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220402152347950.png)

- 对于i=3，也就是容量为11-5的背包，将会在10哪里变一下![image-20220402152627761](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220402152627761.png)

代码：

![image-20220402152728398](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220402152728398.png)

#### [1049. Last Stone Weight II](https://leetcode-cn.com/problems/last-stone-weight-ii/)

难度中等419收藏分享切换为中文接收动态反馈

You are given an array of integers `stones` where `stones[i]` is the weight of the `ith` stone.

We are playing a game with the stones. On each turn, we choose any two stones and smash them together. Suppose the stones have weights `x` and `y` with `x <= y`. The result of this smash is:

- If `x == y`, both stones are destroyed, and
- If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.

At the end of the game, there is **at most one** stone left.

Return *the smallest possible weight of the left stone*. If there are no stones left, return `0`.

 

**Example 1:**

```
Input: stones = [2,7,4,1,8,1]
Output: 1
Explanation:
We can combine 2 and 4 to get 2, so the array converts to [2,7,1,8,1] then,
we can combine 7 and 8 to get 1, so the array converts to [2,1,1,1] then,
we can combine 2 and 1 to get 1, so the array converts to [1,1,1] then,
we can combine 1 and 1 to get 0, so the array converts to [1], then that's the optimal value.
```

**Example 2:**

```
Input: stones = [31,26,33,21,40]
Output: 5
```

思路：

- 将石头尽量分为重量相同的两堆，最优解就是这道题的答案

- 物品的重量等价于价值

- 动态规划五部曲

  - 确定dp数组和下标含义：容量为j的背包，最多可以放dp[j]的物品

  - 确定递推公式：dp[j]=max(dp[j],dp[j-stones[i]]+stones[i])

    - dp[j-stones[i]] 代表容量为j-stones[i]的背包，最大负重

  - 初始化dp数组：全部初始化为0，长度是总重量的一半

  - 确定遍历顺序：一维数组倒序遍历

  - 举例：[2,4,1,1], half = 4

    <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20210121115805904.jpg" alt="1049.最后一块石头的重量II" style="zoom:50%;" />

    最后dp[target]里是容量为target的背包所能背的最大重量。

    那么分成两堆石头，一堆石头的总重量是dp[target]，另一堆就是sum - dp[target]。

    相撞之后剩下的最小石头重量就是 (sum - dp[target]) - dp[target]

- 前一题是问是否能装满，这个是最多装多少，所以是sum-dp[half]-dp[half]

代码：

![image-20220402180250756](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220402180250756.png)

#### [494. Target Sum](https://leetcode-cn.com/problems/target-sum/)

难度中等1143收藏分享切换为中文接收动态反馈

You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

- For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

 

**Example 1:**

```
Input: nums = [1,1,1,1,1], target = 3
Output: 5
Explanation: There are 5 ways to assign symbols to make the sum of nums be target 3.
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3
```

**Example 2:**

```
Input: nums = [1], target = 1
Output: 1
```

思路：

假设有加号的部分叫x，有减号的部分叫sum-x

我们知道x-(sum-x)=target

所以x=(target+sum)/2

- 确定dp数组及其下标
  - dp[j]表示装满容量为j的背包，有dp[j]种方法
  - 不同于之前最多能装多少，这里是有方法的数目
- 确定递推公式
  - 假如我们目标是5，我们有一个1，那么就有dp[4]种方法
  - 同理，如果有2，就有dp[3]种方法.....
  - 所以要求dp[j], 对于i从0~j进行遍历; dp[j] += dp[j-nums[i]]
- 初始化dp
  - 对于dp[0]初始化为1，代表装满容量为0的背包的方法是1，什么都不放
  - 对于其他的dp[j]初始化为0
- 确定遍历循序
  - 外循环正序
  - 内循环倒序
- 举例推导dp数组
  - nums: [1, 1, 1, 1, 1], S: 3
  - 我们可以知道加号的部分是（5+3）//2=4
  - 也就是我们要凑出来一个`+4`和一个`-1`
  - <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20210125120743274.jpg" alt="494.目标和" style="zoom:50%;" />

代码：

- 注意边界条件，如果target的绝对值太大，比整个list求和都大，不可以；或者全是加号的part不是整除，也是不行的。

> 这题的边界条件很多，要小心

- 注意内循环的上限是add_part,不是target

![image-20220402184734081](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220402184734081.png)

#### [474. Ones and Zeroes](https://leetcode-cn.com/problems/ones-and-zeroes/)

难度中等680收藏分享切换为中文接收动态反馈

You are given an array of binary strings `strs` and two integers `m` and `n`.

Return *the size of the largest subset of `strs` such that there are **at most*** `m` `0`*'s and* `n` `1`*'s in the subset*.

A set `x` is a **subset** of a set `y` if all elements of `x` are also elements of `y`.

 

**Example 1:**

```
Input: strs = ["10","0001","111001","1","0"], m = 5, n = 3
Output: 4
Explanation: The largest subset with at most 5 0's and 3 1's is {"10", "0001", "1", "0"}, so the answer is 4.
Other valid but smaller subsets include {"0001", "1"} and {"10", "1", "0"}.
{"111001"} is an invalid subset because it contains 4 1's, greater than the maximum of 3.
```

**Example 2:**

```
Input: strs = ["10","0","1"], m = 1, n = 1
Output: 2
Explanation: The largest subset is {"0", "1"}, so the answer is 2.
```

思路：

- **本题中strs 数组里的元素就是物品，每个物品都是一个！**

  **而m 和 n相当于是一个背包，两个维度的背包**,所以这回是dp[i] [j]

  所以这是一个两个维度的01背包

- 确定dp数组和下标的意义

  - dp[i] [j]代表最多有i个0和j个1的这个子集的长度

- 递推式

  - dp[i] [j]纳入一个str，而这个str种有n_0个0和n_1个1，那么dp[i] [j] = dp[i - str_0] [j - str_1]+1
  - 所以dp[i] [j] = max(dp[i] [j], dp[i - str_0] [j - str_1]+1)

- 确定遍历顺序：

  - 之前一直说内循环要倒序，其实更明确的说是在遍历背包容量时需要从前往后遍历

- 举例

代码：

- 从str种计算字符的个数：![image-20220402201112174](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220402201112174.png)
- ![image-20220402201355039](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220402201355039.png)

### 2.2 完全背包

有N件物品和一个最多能背重量为W的背包。第i件物品的重量是weight[i]，得到的价值是value[i] 。**每件物品都有无限个（也就是可以放入背包多次）**，求解将哪些物品装入背包里物品价值总和最大。

**完全背包和01背包问题唯一不同的地方就是，每种物品有无限件**。

![image-20220402202013982](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220402202013982.png)

![动态规划-完全背包](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20210126104510106.jpg)

**其实还有一个很重要的问题，为什么遍历物品在外层循环，遍历背包容量在内层循环？**

- 01背包中二维dp数组的两个for遍历的先后循序是可以颠倒
- 01背包中一维dp数组的两个for循环先后循序一定是先遍历物品，再遍历背包容量。
- 完全背包种一维dp数组也可以颠倒顺序

**在完全背包中，对于一维dp数组来说，其实两个for循环嵌套顺序同样无所谓！**

#### [518. Coin Change 2](https://leetcode-cn.com/problems/coin-change-2/)

难度中等767

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return *the number of combinations that make up that amount*. If that amount of money cannot be made up by any combination of the coins, return `0`.

You may assume that you have an infinite number of each kind of coin.

The answer is **guaranteed** to fit into a signed **32-bit** integer.

 

**Example 1:**

```
Input: amount = 5, coins = [1,2,5]
Output: 4
Explanation: there are four ways to make up the amount:
5=5
5=2+2+1
5=2+1+1+1
5=1+1+1+1+1
```

**Example 2:**

```
Input: amount = 3, coins = [2]
Output: 0
Explanation: the amount of 3 cannot be made up just with coins of 2.
```

**Example 3:**

```
Input: amount = 10, coins = [10]
Output: 1
```

 思路：

- 本题和纯完全背包不一样，**纯完全背包是能否凑成总金额，而本题是要求凑成总金额的个数！**
- 确定dp数组和下标的含义：dp[j]代表总金额j有dp[j]种组合
- 确定递推公式：与494 Target Sum类似的，对于i从0~j进行遍历; dp[j] += dp[j-nums[i]]
  - 可以理解为对于j这个上限，不断拿各个nums[i]来试着减去，然后看后面的部分有多少种方法。nums[i]一定被使用
- 初始化dp数组：dp[0]  = 1,其余为0
- 确定遍历的顺序
  - 不同于常见的完全背包不考虑两个for循环的顺序
- 举例子
  - 输入: amount = 5, coins = [1, 2, 5] ，dp状态图如下：
  - ![518.零钱兑换II](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20210120181331461.jpg)

代码：

在求装满背包有几种方案的时候，认清遍历顺序是非常关键的。

**如果求组合数就是外层for循环遍历物品，内层for遍历背包**。

**如果求排列数就是外层for遍历背包，内层for循环遍历物品**。

初始化的长度取决于j，j代表容量，dp[j]代表方案的个数

注意dp[0] = 1! 这样递归才能开始

注意内循环是从coins[i]开始的，**内部的起始值很关键**

不能用![image-20220403105426076](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220403105426076.png)这个来判断，因为这样的方式不是0。实际就是不找了，这也是一种方式

![image-20220403105616609](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220403105616609.png)



#### [377. Combination Sum IV](https://leetcode-cn.com/problems/combination-sum-iv/)

难度中等600

Given an array of **distinct** integers `nums` and a target integer `target`, return *the number of possible combinations that add up to* `target`.

The test cases are generated so that the answer can fit in a **32-bit** integer.

 

**Example 1:**

```
Input: nums = [1,2,3], target = 4
Output: 7
Explanation:
The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)
Note that different sequences are counted as different combinations.
```

**Example 2:**

```
Input: nums = [9], target = 3
Output: 0
```

Follow up: What if negative numbers are allowed in the given array? How does it change the problem? What limitation we need to add to the question to allow negative numbers?

思路：

- 这道题就是就排列顺序的，不想上一题是单纯的组合

- 确定dp数组和下标：dp[j], target为j时有dp[j]种排列

- 确定递推公式：dp[j] += dp[j-nums[i]]

  - 看了这么多题，可以得出一个经验性的结论：**对于装满背包的问题，常用的递推式为dp[j] += dp[j-nums[i]]**

- 确定初始化dp[0] = 1,其余为0

- 确定遍历顺序

  - **如果求组合数就是外层for循环遍历物品，内层for遍历背包**。

    **如果求排列数就是外层for遍历背包，内层for循环遍历物品**。

- 举例

  - ![377.组合总和Ⅳ](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20210131174250148.jpg)

- ![image-20220403110931603](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220403110931603.png)

代码：

![image-20220403135530350](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220403135530350.png)

没太搞明白



#### [70. Climbing Stairs](https://leetcode-cn.com/problems/climbing-stairs/)

难度简单2325

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

 

**Example 1:**

```
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**

```
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

思路：

- 可以理解为完全背包
- 确定dp和下标
  - dp[n]代表到n层楼梯有几种走法
- 确定递推式
  - dp[n] += dp[n-j]
  - j只可能是1或者2，也就是走一步还是走两步
- 确定dp数组初始化
  - dp[0] = 1
- 确定遍历顺序
  - 和上一题一样，这是推导排列顺序的问题
  - 所以外层遍历容量，内层是遍历物品
  - 如果是组合就是外层遍历物品，内存遍历容量
  - 为什么？之后要会给别人解释。
- 举例

代码：

![image-20220403220021113](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220403220021113.png)

注意和上一道题目一样，需要进行一个判断才写递推式

#### [322. Coin Change](https://leetcode-cn.com/problems/coin-change/)

难度中等1844

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return *the fewest number of coins that you need to make up that amount*. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

**Example 1:**

```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```

**Example 2:**

```
Input: coins = [2], amount = 3
Output: -1
```

**Example 3:**

```
Input: coins = [1], amount = 0
Output: 0
```

#### [279. Perfect Squares](https://leetcode-cn.com/problems/perfect-squares/)

难度中等1305

Given an integer `n`, return *the least number of perfect square numbers that sum to* `n`.

A **perfect square** is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, `1`, `4`, `9`, and `16` are perfect squares while `3` and `11` are not.

 

**Example 1:**

```
Input: n = 12
Output: 3
Explanation: 12 = 4 + 4 + 4.
```

**Example 2:**

```
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```

#### [139. Word Break](https://leetcode-cn.com/problems/word-break/)

难度中等1518

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

 

**Example 1:**

```
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

**Example 2:**

```
Input: s = "applepenapple", wordDict = ["apple","pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.
```

**Example 3:**

```
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: false
```

### 2.3 背包总结

## 3. 打家劫舍

#### [198. House Robber](https://leetcode-cn.com/problems/house-robber/)

难度中等2034

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return *the maximum amount of money you can rob tonight **without alerting the police***.

 

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
```

**Example 2:**

```
Input: nums = [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.
```

#### [213. House Robber II](https://leetcode-cn.com/problems/house-robber-ii/)

难度中等988

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return *the maximum amount of money you can rob tonight **without alerting the police***.

 

**Example 1:**

```
Input: nums = [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.
```

**Example 2:**

```
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
```

**Example 3:**

```
Input: nums = [1,2,3]
Output: 3
```

#### [337. House Robber III](https://leetcode-cn.com/problems/house-robber-iii/)

难度中等1222

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called `root`.

Besides the `root`, each house has one and only one parent house. After a tour, the smart thief realized that all houses in this place form a binary tree. It will automatically contact the police if **two directly-linked houses were broken into on the same night**.

Given the `root` of the binary tree, return *the maximum amount of money the thief can rob **without alerting the police***.

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/rob1-tree.jpg)

```
Input: root = [3,2,3,null,3,null,1]
Output: 7
Explanation: Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/rob2-tree.jpg)

```
Input: root = [3,4,5,1,3,null,1]
Output: 9
Explanation: Maximum amount of money the thief can rob = 4 + 5 = 9.
```

 

## 4. 股票问题

#### [121. Best Time to Buy and Sell Stock](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

难度简单2250

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return *the maximum profit you can achieve from this transaction*. If you cannot achieve any profit, return `0`.

 

**Example 1:**

```
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
```

**Example 2:**

```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
```

## 5. 子序列问题

### 5.1 子序列不连续

### 5.2 子序列连续

### 5.3 编辑距离

### 5.4 回文