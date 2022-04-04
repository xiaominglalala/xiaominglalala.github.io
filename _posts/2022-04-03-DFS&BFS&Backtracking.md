---
layout:     post
title:      DFS+BFS+Backtracking
subtitle:   
date:       2022-04-3
author:     Ethan
header-img: img/6.jpg
catalog: true
tags:
    - Leetcode
    - DFS
    - BFS
    - Backtracking

---

## 深度优先搜索

#### [695. 岛屿的最大面积](https://leetcode-cn.com/problems/max-area-of-island/)

给你一个大小为 `m x n` 的二进制矩阵 `grid` 。

**岛屿** 是由一些相邻的 `1` (代表土地) 构成的组合，这里的「相邻」要求两个 `1` 必须在 **水平或者竖直的四个方向上** 相邻。你可以假设 `grid` 的四个边缘都被 `0`（代表水）包围着。

岛屿的面积是岛上值为 `1` 的单元格的数目。

计算并返回 `grid` 中最大的岛屿面积。如果没有岛屿，则返回面积为 `0` 。

 

**示例 1：**

<img src="https://assets.leetcode.com/uploads/2021/05/01/maxarea1-grid.jpg" alt="img" style="zoom:50%;" />

```
输入：grid = [[0,0,1,0,0,0,0,1,0,0,0,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,1,1,0,1,0,0,0,0,0,0,0,0],[0,1,0,0,1,1,0,0,1,0,1,0,0],[0,1,0,0,1,1,0,0,1,1,1,0,0],[0,0,0,0,0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,0,0,0,0,0,0,1,1,0,0,0,0]]
输出：6
解释：答案不应该是 11 ，因为岛屿只能包含水平或垂直这四个方向上的 1 。
```

**示例 2：**

```
输入：grid = [[0,0,0,0,0,0,0,0]]
输出：0
```

------

**思路**：

- 使用递归的方法，每次到达一块土地，如果当前位置没有超过边界，就朝四个方向探索
- 每次经过一次土地，就把他的值设置为0，避免被其他的四方向探索所访问
- ![image-20211230122035377](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211230122035377.png)

**代码**：

![image-20211230122224752](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211230122224752.png)



![image-20211230123101412](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211230123101412.png)

![image-20211230123150154](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211230123150154.png)



------

#### [200. 岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

难度中等1476

给你一个由 `'1'`（陆地）和 `'0'`（水）组成的的二维网格，请你计算网格中岛屿的数量。

岛屿总是被水包围，并且每座岛屿只能由水平方向和/或竖直方向上相邻的陆地连接形成。

此外，你可以假设该网格的四条边均被水包围。

 

**示例 1：**

```
输入：grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
输出：1
```

**示例 2：**

```
输入：grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
输出：3
```

思路：

和上一题基本一致，只需要把str变为int，然后判断岛屿面积>=1

代码：

![image-20211230171121082](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211230171121082.png)



![image-20211230171500102](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211230171500102.png)

![image-20211230171526967](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211230171526967.png)

#### 547. [省份数量](https://leetcode-cn.com/problems/number-of-provinces/)

有 `n` 个城市，其中一些彼此相连，另一些没有相连。如果城市 `a` 与城市 `b` 直接相连，且城市 `b` 与城市 `c` 直接相连，那么城市 `a` 与城市 `c` 间接相连。

**省份** 是一组直接或间接相连的城市，组内不含其他没有相连的城市。

给你一个 `n x n` 的矩阵 `isConnected` ，其中 `isConnected[i][j] = 1` 表示第 `i` 个城市和第 `j` 个城市直接相连，而 `isConnected[i][j] = 0` 表示二者不直接相连。

返回矩阵中 **省份** 的数量。

 

**示例 1：**

<img src="https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg" alt="img" style="zoom:50%;" />

```
输入：isConnected = [[1,1,0],[1,1,0],[0,0,1]]
输出：2
```

**示例 2：**

<img src="https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg" alt="img" style="zoom:50%;" />

```
输入：isConnected = [[1,0,0],[0,1,0],[0,0,1]]
输出：3
```

------

思路：

- 深度优先搜索

  - 遍历所有城市，对于每个城市，如果该城市尚未被访问过，则从该城市开始深度优先搜索，通过矩阵 isConnected 得到与该城市直接相连的城市有哪些，这些城市和该城市属于同一个连通分量，然后对这些城市继续深度优先搜索，直到同一个连通分量的所有城市都被访问到，即可得到一个省份。遍历完全部城市以后，即可得到连通分量的总数，即省份的总数。

    

代码：

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211206152757416.png" alt="image-20211206152757416" style="zoom:50%;" />



#### [207. 课程表](https://leetcode-cn.com/problems/course-schedule/)

难度中等1067

你这个学期必须选修 `numCourses` 门课程，记为 `0` 到 `numCourses - 1` 。

在选修某些课程之前需要一些先修课程。 先修课程按数组 `prerequisites` 给出，其中 `prerequisites[i] = [ai, bi]` ，表示如果要学习课程 `ai` 则 **必须** 先学习课程 `bi` 。

- 例如，先修课程对 `[0, 1]` 表示：想要学习课程 `0` ，你需要先完成课程 `1` 。

请你判断是否可能完成所有课程的学习？如果可以，返回 `true` ；否则，返回 `false` 。

 

**示例 1：**

```
输入：numCourses = 2, prerequisites = [[1,0]]
输出：true
解释：总共有 2 门课程。学习课程 1 之前，你需要完成课程 0 。这是可能的。
```

**示例 2：**

```
输入：numCourses = 2, prerequisites = [[1,0],[0,1]]
输出：false
解释：总共有 2 门课程。学习课程 1 之前，你需要先完成课程 0 ；并且学习课程 0 之前，你还应先完成课程 1 。这是不可能的。
```

#### [417. 太平洋大西洋水流问题](https://leetcode-cn.com/problems/pacific-atlantic-water-flow/)

难度中等321

给定一个 `m x n` 的非负整数矩阵来表示一片大陆上各个单元格的高度。“太平洋”处于大陆的左边界和上边界，而“大西洋”处于大陆的右边界和下边界。

规定水流只能按照上、下、左、右四个方向流动，且只能从高到低或者在同等高度上流动。

请找出那些水流既可以流动到“太平洋”，又能流动到“大西洋”的陆地单元的坐标。

 

**提示：**

1. 输出坐标的顺序不重要
2. *m* 和 *n* 都小于150

 

**示例：**

 

```
给定下面的 5x5 矩阵:

  太平洋 ~   ~   ~   ~   ~ 
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * 大西洋

返回:

[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (上图中带括号的单元).
```

#### [337. 打家劫舍 III](https://leetcode-cn.com/problems/house-robber-iii/)

难度中等1083

在上次打劫完一条街道之后和一圈房屋后，小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为“根”。 除了“根”之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果两个直接相连的房子在同一天晚上被打劫，房屋将自动报警。

计算在不触动警报的情况下，小偷一晚能够盗取的最高金额。

**示例 1:**

```
输入: [3,2,3,null,3,null,1]

     3
    / \
   2   3
    \   \ 
     3   1

输出: 7 
解释: 小偷一晚能够盗取的最高金额 = 3 + 3 + 1 = 7.
```

**示例 2:**

```
输入: [3,4,5,1,3,null,1]

     3
    / \
   4   5
  / \   \ 
 1   3   1

输出: 9
解释: 小偷一晚能够盗取的最高金额 = 4 + 5 = 9.
```



## 广度优先搜索

#### [322. 零钱兑换](https://leetcode-cn.com/problems/coin-change/)

难度中等1625

给你一个整数数组 `coins` ，表示不同面额的硬币；以及一个整数 `amount` ，表示总金额。

计算并返回可以凑成总金额所需的 **最少的硬币个数** 。如果没有任何一种硬币组合能组成总金额，返回 `-1` 。

你可以认为每种硬币的数量是无限的。

 

**示例 1：**

```
输入：coins = [1, 2, 5], amount = 11
输出：3 
解释：11 = 5 + 5 + 1
```

**示例 2：**

```
输入：coins = [2], amount = 3
输出：-1
```

**示例 3：**

```
输入：coins = [1], amount = 0
输出：0
```

**示例 4：**

```
输入：coins = [1], amount = 1
输出：1
```

**示例 5：**

```
输入：coins = [1], amount = 2
输出：2
```



#### [07. 接雨水 II](https://leetcode-cn.com/problems/trapping-rain-water-ii/)

难度困难548

给你一个 `m x n` 的矩阵，其中的值均为非负整数，代表二维高度图每个单元的高度，请计算图中形状最多能接多少体积的雨水。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/04/08/trap1-3d.jpg)

```
输入: heightMap = [[1,4,3,1,3,2],[3,2,1,3,2,4],[2,3,3,2,3,1]]
输出: 4
解释: 下雨后，雨水将会被上图蓝色的方块中。总的接雨水量为1+2+1=4。
```

**示例 2:**

![img](https://assets.leetcode.com/uploads/2021/04/08/trap2-3d.jpg)

```
输入: heightMap = [[3,3,3,3,3],[3,2,2,2,3],[3,2,1,2,3],[3,2,2,2,3],[3,3,3,3,3]]
输出: 10
```

#### [207. 课程表](https://leetcode-cn.com/problems/course-schedule/)

难度中等1067

你这个学期必须选修 `numCourses` 门课程，记为 `0` 到 `numCourses - 1` 。

在选修某些课程之前需要一些先修课程。 先修课程按数组 `prerequisites` 给出，其中 `prerequisites[i] = [ai, bi]` ，表示如果要学习课程 `ai` 则 **必须** 先学习课程 `bi` 。

- 例如，先修课程对 `[0, 1]` 表示：想要学习课程 `0` ，你需要先完成课程 `1` 。

请你判断是否可能完成所有课程的学习？如果可以，返回 `true` ；否则，返回 `false` 。

 

**示例 1：**

```
输入：numCourses = 2, prerequisites = [[1,0]]
输出：true
解释：总共有 2 门课程。学习课程 1 之前，你需要完成课程 0 。这是可能的。
```

**示例 2：**

```
输入：numCourses = 2, prerequisites = [[1,0],[0,1]]
输出：false
解释：总共有 2 门课程。学习课程 1 之前，你需要先完成课程 0 ；并且学习课程 0 之前，你还应先完成课程 1 。这是不可能的。
```

#### [279. 完全平方数](https://leetcode-cn.com/problems/perfect-squares/)

难度中等1177

给定正整数 *n*，找到若干个完全平方数（比如 `1, 4, 9, 16, ...`）使得它们的和等于 *n*。你需要让组成和的完全平方数的个数最少。

给你一个整数 `n` ，返回和为 `n` 的完全平方数的 **最少数量** 。

**完全平方数** 是一个整数，其值等于另一个整数的平方；换句话说，其值等于一个整数自乘的积。例如，`1`、`4`、`9` 和 `16` 都是完全平方数，而 `3` 和 `11` 不是。

 

**示例 1：**

```
输入：n = 12
输出：3 
解释：12 = 4 + 4 + 4
```

**示例 2：**

```
输入：n = 13
输出：2
解释：13 = 4 + 9
```

## 回溯法

- 一种通过探索所有可能的候选解来找出所有的解的算法。如果候选解被确认不是一个解（或者至少不是最后一个解），回溯算法会通过在上一步进行一些变化抛弃该解，即回溯并且再次尝试。
- 回溯法修改一般有两种情况，一种是修改最后一位输出，比如排列组合；一种是修改访问标记，比如矩阵里搜字符串。



#### [77. 组合](https://leetcode-cn.com/problems/combinations/)

难度中等786

给定两个整数 `n` 和 `k`，返回范围 `[1, n]` 中所有可能的 `k` 个数的组合。

你可以按 **任何顺序** 返回答案。

**示例 1：**

```
输入：n = 4, k = 2
输出：
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

**示例 2：**

```
输入：n = 1, k = 1
输出：[[1]]
```

------

- 回溯法三部曲
  - 递归函数的变量
    - 在这道题中首先需要变量存放符合条件的一个结果`result`
    - 其次需要存放符合条件的结果的结合：`result_list`
    - 此外，需要一个变量来确定从哪里开始遍历集合：`start_index`放在backtracking（回溯）函数里面。
    - n是数的范围，k是每个组合的长度
    - ![image-20211208114649518](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211208114649518.png)
  - 递归的终止条件
    - 当达到终止条件，此时把result保存至result_list之中，并终止此次递归
    - 在这个问题中，当目前寻找的组合的长度已经达到k了，说明已经找到底了，该回溯了，终止此次递归
    - ![image-20211208120905762](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211208120905762.png)
  - 单层搜索的过程
    - 第一层for循环，横向遍历所有的元素
    - 第二层for循环进行递归
    - ![image-20211208122805788](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211208122805788.png)
    - 所谓的回溯就是`result.pop()`，会让result从[1,2]变为[1], 之后再变成[1, 3]
- 剪枝优化
  - **如果for循环选择的起始位置之后的元素个数 已经不足 我们需要的元素个数了，那么就没有必要搜索了**
  - 已经选择的元素个数：`len(result)`;
  - 还需要的元素个数为: `k - len(result)`;
  - 在集合n中至多要从该起始位置 : `n - (k - len(result)) + 1`，开始遍历。
  - 为什么有个+1呢，因为包括起始位置，我们要是一个左闭的集合。而python的range不包含右节点，所以是+2
- 代码
  - ![image-20211208140606999](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211208140606999.png)

#### [17. 电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

难度中等1634收藏分享切换为英文接收动态反馈

给定一个仅包含数字 `2-9` 的字符串，返回所有它能表示的字母组合。答案可以按 **任意顺序** 返回。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/200px-telephone-keypad2svg.png)

 

**示例 1：**

```
输入：digits = "23"
输出：["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

**示例 2：**

```
输入：digits = ""
输出：[]
```

**示例 3：**

```
输入：digits = "2"
输出：["a","b","c"]
```

------

**分析：**

- 这道题主要两个问题
  - 解决数字和字母的对应关系，并处理异常情况。因为说了只有2~9的数字，所以只要考虑空的输入即可。
    - 在`self.init`里面写好对应关系
  - 处理多个for循环，使用回溯法三部曲
- 回溯法三部曲
  - 确定变量
  - 确定递归终止条件
  - 确定单次搜索的内容
- 确定变量
  - 存储单次结果`result`
  - 存储所有的结果`result_list`

**代码：**

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211208142700932.png" alt="image-20211208142700932" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211208142737844.png" alt="image-20211208142737844" style="zoom:50%;" />

- 

#### [39. 组合总和](https://leetcode-cn.com/problems/combination-sum/)

难度中等1661收藏分享切换为英文接收动态反馈

给定一个**无重复元素**的正整数数组 `candidates` 和一个正整数 `target` ，找出 `candidates` 中所有可以使数字和为目标数 `target` 的唯一组合。

`candidates` 中的数字可以无限制重复被选取。如果至少一个所选数字数量不同，则两种组合是唯一的。 

对于给定的输入，保证和为 `target` 的唯一组合数少于 `150` 个。

 

**示例 1：**

```
输入: candidates = [2,3,6,7], target = 7
输出: [[7],[2,2,3]]
```

**示例 2：**

```
输入: candidates = [2,3,5], target = 8
输出: [[2,2,2,2],[2,3,3],[3,5]]
```

**示例 3：**

```
输入: candidates = [2], target = 1
输出: []
```

**示例 4：**

```
输入: candidates = [1], target = 1
输出: [[1]]
```

**示例 5：**

```
输入: candidates = [1], target = 2
输出: [[1,1]]
```

------

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20201223170730367.png" alt="39.组合总和" style="zoom: 33%;" />





#### [46. 全排列](https://leetcode-cn.com/problems/permutations/)

难度中等1673

给定一个不含重复数字的数组 `nums` ，返回其 **所有可能的全排列** 。你可以 **按任意顺序** 返回答案。

 

**示例 1：**

```
输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

**示例 2：**

```
输入：nums = [0,1]
输出：[[0,1],[1,0]]
```

**示例 3：**

```
输入：nums = [1]
输出：[[1]]
```

------

**分析：**

- ![image.png](https://pic.leetcode-cn.com/0bf18f9b86a2542d1f6aa8db6cc45475fce5aa329a07ca02a9357c2ead81eec1-image.png)

#### [51. N 皇后](https://leetcode-cn.com/problems/n-queens/)

难度困难1116

**n 皇后问题** 研究的是如何将 `n` 个皇后放置在 `n×n` 的棋盘上，并且使皇后彼此之间不能相互攻击。

给你一个整数 `n` ，返回所有不同的 **n 皇后问题** 的解决方案。

每一种解法包含一个不同的 **n 皇后问题** 的棋子放置方案，该方案中 `'Q'` 和 `'.'` 分别代表了皇后和空位。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

```
输入：n = 4
输出：[[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
解释：如上图所示，4 皇后问题存在两个不同的解法。
```

**示例 2：**

```
输入：n = 1
输出：[["Q"]]
```

