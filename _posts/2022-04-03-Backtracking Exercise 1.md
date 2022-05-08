---
layout:     post
title:      Backtracking Exercise 1
subtitle:   
date:       2022-04-13
author:     Ethan
header-img: img/2.jpg
catalog: true
tags:
    - Leetcode
    - Backtracking
---

## Backtracking Exercise 1

- 回溯算法是一种通过不断 尝试 ，搜索一个问题的一个解或者 所有解 的方法。在求解的过程中，如果继续求解不能得到题目要求的结果，就需要 回退 到上一步尝试新的求解路径。回溯算法的核心思想是：在一棵 隐式的树（看不见的树） 上进行一次深度优先遍历。
- 问「一个问题 **所有的** 解」一般考虑使用回溯算法。因此回溯算法也叫「暴力搜索」，但不同于最粗暴的多个 `for` 循环，回溯算法是有方向的遍历。
- 在一条路上错误了，就会跳过当前路径，所以比纯暴力快
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

思路：

> 面试的时候也要和面试官先说brute force

- 很容易想到brute force，但是几个k就需要几层for循环

- 使用回溯法存在两种，是否剪枝（Pruning）

  - 如果不pruning

    ![77.组合1](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20201123195242899.png)

  - 如果purning。稍微改变一下题目要求，变成长度为4的组合。**如果for循环选择的起始位置之后的元素个数 已经不足 我们需要的元素个数了，那么就没有必要搜索了**。

    1. 已经有的元素个数：result.size();
    2. 还需要的元素个数为: k - result.size();
    3. 在集合n中至多要从该起始位置 : n - (k - result.size()) + 1，开始遍历

    为什么有个+1呢，因为包括起始位置，我们要是一个左闭的集合。

    <img src="https://img-blog.csdnimg.cn/20210130194335207.png" alt="77.组合4" style="zoom:50%;" />

  

- 回溯法三部曲

  - 递归函数的返回值和参数

    - 存放符合条件的一个结果`result`

    - 存放符合条件的结果的集合：`result_list`

    - 此外，需要一个变量来确定从哪里开始遍历集合：`start_index`放在backtracking（回溯）函数里面。![image-20220418182600028](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220418182600028.png)

      

  - 递归的终止条件

    - 当达到终止条件，此时把result保存至result_list之中，并终止此次递归
    - 在这个问题中，当目前寻找的组合的长度已经达到题目中给出的k，也就是2。说明该回溯了，终止此次递归

  - 单层搜索的过程

    - 第一层for循环，横向遍历所有的元素
    - 第二层for循环，进行递归，纵向遍历
    - ![image-20211208122805788](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211208122805788.png)
    - 所谓的回溯就是`result.pop()`，会让result从[1,2]变为[1], 之后再变成[1, 3]

- 剪枝优化

  - **如果for循环选择的起始位置之后的元素个数 已经不足 我们需要的元素个数了，那么就没有必要搜索了**
  - 已经选择的元素个数：`len(result)`;
  - 还需要的元素个数为: `k - len(result)`;
  - 在集合n中至多选择位置 : `n - (k - len(result)) + 1`，把他放入result里，并从他这里开始遍历
  - 为什么有个+1呢，因为包括起始位置，我们要是一个左闭的集合。而python的range不包含右节点，所以是+2
  - 比如对于n=4，k=4，我们已经拿到2位了。n要从4 -（4-2）+2=4，也就是至多从num=3开始遍历。因为4是圆括号，娶不到
  - <img src="https://img-blog.csdnimg.cn/20210130194335207.png" alt="77.组合4" style="zoom:50%;" />
  - 比如n=4，k=2，；yi4-(2-0)+2=4，至多从num = 3;4-(2-1)+2=5，至多从num=4 
  - ![image-20220418194034820](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220418194034820.png)

- 代码

  没有剪枝

  ![image-20220418184406198](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220418184406198.png)

  ![image-20220418184722906](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220418184722906.png)

  在获得了[1,2]之后，才会执行8，把它放入result_list

  然后才会执行9 return；然后才会执行14，把2给pop出去

  剪枝：

  ![image-20211208140606999](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211208140606999.png)

#### [216. 组合总和 III](https://leetcode-cn.com/problems/combination-sum-iii/)

难度中等457

找出所有相加之和为 `n` 的 `k` 个数的组合，且满足下列条件：

- 只使用数字1到9
- 每个数字 **最多使用一次** 

返回 *所有可能的有效组合的列表* 。该列表不能包含相同的组合两次，组合可以以任何顺序返回。

 

**示例 1:**

```
输入: k = 3, n = 7
输出: [[1,2,4]]
解释:
1 + 2 + 4 = 7
没有其他符合的组合了。
```

**示例 2:**

```
输入: k = 3, n = 9
输出: [[1,2,6], [1,3,5], [2,3,4]]
解释:
1 + 2 + 6 = 9
1 + 3 + 5 = 9
2 + 3 + 4 = 9
没有其他符合的组合了。
```

**示例 3:**

```
输入: k = 4, n = 1
输出: []
解释: 不存在有效的组合。
在[1,9]范围内使用4个不同的数字，我们可以得到的最小和是1+2+3+4 = 10，因为10 > 1，没有有效的组合。
```

 

**提示:**

- `2 <= k <= 9`
- `1 <= n <= 60`

思路：

- 相比起上一题, 这题只是增加了要满足列表内元素总和的要求
- 首先是确定返回的结果和回溯所用到的参数
  - 和上一题一样，需要result来存储当前的结果，result_list来存储所有结果
  - k位题目中的列表内元素个数；n为所需要的和；start_index是下一次for循环搜索的起始位置；sum是当前的列表求和
- 然后是确定终止条件
  - 列表内元素个数k限制树的深度，因为就取k个元素，树再往下深了没有意义。如果len(result)和 k相等了，就终止
  - 如果此时sum(result)和n一样，则拿当前结果
  - ![216.组合总和III](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20201123195717975.png)
- 那么剪枝操作其实很容易想到，就是如果当前的sum(result)已经大于k，而len(result) <=k; 往后面遍历就没有必要了，就可以直接剪掉了
  - ![216.组合总和III1](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/2020112319580476.png)
  - 在这里，很明显，当sum>4, 就没有后续的必要了
  - i <= 9 - (k - result.size()) + 1就可以；在python的range应该是9 - (k - result.size()) + 2

代码：

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220419111919584.png" alt="image-20220419111919584" style="zoom:50%;" />

因为值只能选择1~9，所以初始化的时候也是1开始

对于k=3，n=7

比如第一次，找到了[1,2,3]，再找就是4，就会跳到16，17，pop出去3，result减去4.

再继续当前的for循环，因为还没走到末尾，从[1,2,4]

发现[1,2,4]ok。再跳出去[1,2,5]。最后[1,2,9]

然后第一个for循环的第二位的for就算是跑完了，开始[1,3]

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
  - 使用hash table建立对应关系
  - 处理多个for循环，使用回溯法三部曲
  
- 回溯法三部曲
  - 确定变量
  
    - 存储单次结果`result`
    - 存储所有的结果`result_list`
  
  - 确定递归终止条件
  
    - 例如输入用例"23"，两个数字，那么根节点往下递归两层就可以了，叶子节点就是要收集的结果集。
  
      那么终止条件就是如果index 等于 输入的数字个数（digits.size）了
  
  - 确定单次搜索的内容
  
    - ![image-20220419114142775](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220419114142775.png)
    - **注意这里for循环，可不像是在[回溯算法：求组合问题！ (opens new window)](https://programmercarl.com/0077.组合.html)和[回溯算法：求组合总和！ (opens new window)](https://programmercarl.com/0216.组合总和III.html)中从startIndex开始遍历的**。
    - **因为本题每一个数字代表的是不同集合，也就是求不同集合之间的组合，而[77. 组合 (opens new window)](https://programmercarl.com/0077.组合.html)和[216.组合总和III (opens new window)](https://programmercarl.com/0216.组合总和III.html)都是是求同一个集合中的组合！**
    - 注意：输入1 * #按键等等异常情况。**但是要知道会有这些异常，如果是现场面试中，一定要考虑到！**
  
  - ![17. 电话号码的字母组合](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20201123200304469.png)

**代码：**

![image-20220419115514129](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220419115514129.png)



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

思路：

- 虽然可以无限选取，但是不能存在0.下面提示：1 <= candidates[i] <= 200
- 本题没有数量要求，可以无限重复，但是有总和的限制，所以间接的也是有个数的限制。
- 不想216和77对于元素个数有限制，这里没有，所以只要总和超过了就要return

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20201223170730367.png" alt="39.组合总和" style="zoom: 33%;" />

剪枝优化：

- 其实如果已经知道下一层的sum会大于target，就没有必要进入下一层递归了。
- **对总集合排序之后，如果下一层的sum（就是本层的 sum + candidates[i]）已经大于target，就可以结束本轮for循环的遍历**。
- 也就是再取3不行后，就别取5了
- **在求和问题中，排序之后加剪枝是常见的套路！**
- <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20201223170809182.png" alt="39.组合总和1" style="zoom: 33%;" />

代码：

![image-20220419122104102](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220419122104102.png)

![image-20220419123336263](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220419123336263.png)

#### [40. Combination Sum II](https://leetcode-cn.com/problems/combination-sum-ii/)

难度中等927

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

 

**Example 1:**

```
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

**Example 2:**

```
Input: candidates = [2,5,2,1,2], target = 5
Output: 
[
[1,2,2],
[5]
]
```

 

**Constraints:**

- `1 <= candidates.length <= 100`
- `1 <= candidates[i] <= 50`
- `1 <= target <= 30`

思路：

- 本题candidates 中的每个数字在每个组合中只能使用一次。本题数组candidates的元素是有重复的，而[39.组合总和 (opens new window)](https://programmercarl.com/0039.组合总和.html)是无重复元素的数组candidates

- **本题的难点在于区别2中：集合（数组candidates）有重复元素，但还不能有重复的组合**

- 解决方案是同一树层不可以取相同的，同一树枝可以

- **强调一下，树层去重的话，需要对数组排序！**

- 选择过程树形结构如图所示：

  ![40.组合总和II](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20201123202736384.png)

- 对于去重

- **如果`candidates[i] == candidates[i - 1]` 并且 `used[i - 1] == false`，就说明：前一个树枝，使用了candidates[i - 1]，也就是说同一树层使用过candidates[i - 1]**。此时for循环里就应该做continue的操作。

- ![40.组合总和II1](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20201123202817973.png)

- **注意sum + candidates[i] <= target为剪枝操作**

代码：

![image-20220419132322419](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220419132322419.png)

- 可以看到不是可以重复取的，都是i+1作为下一个index，只有可以重复取得，像是39，才是i

![image-20220419133831722](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220419133831722.png)

#### [131. Palindrome Partitioning](https://leetcode-cn.com/problems/palindrome-partitioning/) & [剑指 Offer II 086. 分割回文子字符串](https://leetcode-cn.com/problems/M99OJA/)

难度中等1088

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

 

**Example 1:**

```
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
```

**Example 2:**

```
Input: s = "a"
Output: [["a"]]
```

 

**Constraints:**

- `1 <= s.length <= 16`
- `s` contains only lowercase English letters.

思路：

- **其实切割问题类似组合问题**
- ![131.分割回文串](https://code-thinking.cdn.bcebos.com/pics/131.分割回文串.jpg)
- 递归用来纵向遍历，for循环用来横向遍历
- 判断回文子串
  - 可以使用双指针法，一个指针从前向后，一个指针从后先前，如果前后指针所指向的元素是相等的，就是回文字符串了。

代码：

![image-20220419170026948](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220419170026948.png)

#### [93. Restore IP Addresses](https://leetcode-cn.com/problems/restore-ip-addresses/)& [剑指 Offer II 087. 复原 IP ](https://leetcode-cn.com/problems/0on3uN/)

难度中等876

A **valid IP address** consists of exactly four integers separated by single dots. Each integer is between `0` and `255` (**inclusive**) and cannot have leading zeros.

- For example, `"0.1.2.201"` and `"192.168.1.1"` are **valid** IP addresses, but `"0.011.255.245"`, `"192.168.1.312"` and `"192.168@1.1"` are **invalid** IP addresses.

Given a string `s` containing only digits, return *all possible valid IP addresses that can be formed by inserting dots into* `s`. You are **not** allowed to reorder or remove any digits in `s`. You may return the valid IP addresses in **any** order.

 

**Example 1:**

```
Input: s = "25525511135"
Output: ["255.255.11.135","255.255.111.35"]
```

**Example 2:**

```
Input: s = "0000"
Output: ["0.0.0.0"]
```

**Example 3:**

```
Input: s = "101023"
Output: ["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
```

 

**Constraints:**

- `1 <= s.length <= 20`
- `s` consists of digits only.

思路：

- 这是切割问题，**切割问题就可以使用回溯搜索法把所有可能性搜出来**，和刚做过的[131.分割回文串 (opens new window)](https://programmercarl.com/0131.分割回文串.html)就十分类似了。

- ![93.复原IP地址](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20201123203735933.png)

- 终止条件和[131.分割回文串 (opens new window)](https://programmercarl.com/0131.分割回文串.html)情况就不同了，本题明确要求只会分成4段，所以不能用切割线切到最后作为终止条件，而是分割的段数作为终止条件。然后验证一下第四段是否合法，如果合法就加入到结果集里

- 在[131.分割回文串 (opens new window)](https://programmercarl.com/0131.分割回文串.html)中已经讲过在循环遍历中如何截取子串。

  在`for (int i = startIndex; i < s.size(); i++)`循环中 [startIndex, i] 这个区间就是截取的子串，需要判断这个子串是否合法。

  如果合法就在字符串后面加上符号`.`表示已经分割。

  如果不合法就结束本层循环，如图中剪掉的分支：

- 然后就是递归和回溯的过程：

  递归调用时，下一层递归的startIndex要从i+2开始（因为需要在字符串中加入了分隔符`.`），同时记录分割符的数量pointNum 要 +1。

  回溯的时候，就将刚刚加入的分隔符`.` 删掉就可以了，pointNum也要-1。

- 判断子串是否合法

  - 段位以0为开头的数字不合法，除非本身是0
  - 段位里有非正整数字符不合法
  - 段位如果大于255了不合法


代码：

![image-20220419204907361](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220419204907361.png)

#### [78. Subsets](https://leetcode-cn.com/problems/subsets/)

难度中等1592

Given an integer array `nums` of **unique** elements, return *all possible subsets (the power set)*.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

 

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

**Example 2:**

```
Input: nums = [0]
Output: [[],[0]]
```

 

**Constraints:**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- All the numbers of `nums` are **unique**.

思路：

- 子集问题和[77.组合 (opens new window)](https://programmercarl.com/0077.组合.html)和[131.分割回文串 (opens new window)](https://programmercarl.com/0131.分割回文串.html)又不一样了。**组合问题和分割问题都是收集树的叶子节点，而子集问题是找树的所有节点！**
- 但是子集也是一种组合问题，因为它的集合是无序的，子集{1,2} 和 子集{2,1}是一样的。**那么既然是无序，取过的元素不会重复取，写回溯算法的时候，for就要从startIndex开始，而不是从0开始！**
- 求排列问题的时候，就要从0开始，因为集合是有序的，{1, 2} 和{2, 1}是两个集合
- ![78.子集](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/202011232041348.png)

代码：

![image-20220419211905738](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220419211905738.png)

#### [90. Subsets II](https://leetcode-cn.com/problems/subsets-ii/)

难度中等805

Given an integer array `nums` that may contain duplicates, return *all possible subsets (the power set)*.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

 

**Example 1:**

```
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```

**Example 2:**

```
Input: nums = [0]
Output: [[],[0]]
```

 

**Constraints:**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`

思路：

- 这道题目和[78.子集 (opens new window)](https://programmercarl.com/0078.子集.html)区别就是集合里有重复元素了，而且求取的子集要去重。
- 那么关于回溯算法中的去重问题，**在[40.组合总和II (opens new window)](https://programmercarl.com/0040.组合总和II.html)中已经详细讲解过了，和本题是一个套路**。
- 同一树层不可以取相同的，同一树枝可以
- 树层去重的话，需要对数组排序
- ![90.子集II](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20201124195411977.png)

代码：

![image-20220419234404702](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220419234404702.png)

#### [491. Increasing Subsequences](https://leetcode-cn.com/problems/increasing-subsequences/)

难度中等429

Given an integer array `nums`, return all the different possible increasing subsequences of the given array with ==**at least two elements**.== You may return the answer in **any order**.

The given array may contain duplicates, and two equal integers should also be considered a special case of increasing sequence.

 

**Example 1:**

```
Input: nums = [4,6,7,7]
Output: [[4,6],[4,6,7],[4,6,7,7],[4,7],[4,7,7],[6,7],[6,7,7],[7,7]]
```

**Example 2:**

```
Input: nums = [4,4,3,2,1]
Output: [[4,4]]
```

 

**Constraints:**

- `1 <= nums.length <= 15`
- `-100 <= nums[i] <= 100`

思路：

- 在[90.子集II (opens new window)](https://programmercarl.com/0090.子集II.html)中我们是通过排序，再加一个标记数组来达到去重的目的。

  而本题求自增子序列，是不能对原数组经行排序的，排完序的数组都是自增子序列了。

- 本题给出的示例，还是一个有序数组 [4, 6, 7, 7]，这更容易误导大家按照排序的思路去做了。为了有鲜明的对比，我用[4, 7, 6, 7]这个数组来举例，抽象为树形结构如图：

  ![491. 递增子序列1](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20201124200229824.png)

- 本题收集结果有所不同，题目要求递增子序列大小至少为2

- **同一父节点下的同层上使用过的元素就不能在使用了**

- 注意题目中说了，数值范围[-100,100]，所以完全可以用数组来做哈希。

  

代码：

![image-20220420143531054](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220420143531054.png)

可以使用hash table来去重，因为`-100 <= nums[i] <= 100`

![image-20220420144553016](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220420144553016.png)

但不知道为什么实际跑出来时间更长

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

- ![46.全排列](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20211027181706.png)

- 当收集元素的数组path的大小达到和nums数组一样大的时候，说明找到了一个全排列，也表示到达了叶子节点。

- 这里和[77.组合问题 (opens new window)](https://programmercarl.com/0077.组合.html)、[131.切割问题 (opens new window)](https://programmercarl.com/0131.分割回文串.html)和[78.子集问题 (opens new window)](https://programmercarl.com/0078.子集.html)最大的不同就是for循环里不用startIndex了。

  因为排列问题，每次都要从头开始搜索，例如元素1在[1,2]中已经使用过了，但是在[2,1]中还要再使用一次1。

  **而used数组，其实就是记录此时path里都有哪些元素使用了，一个排列里一个元素只能使用一次**。

- 那天和暴力的区别在哪里？

- 暴力的话，数组长度加一就要多一个for

- 大家此时可以感受出排列问题的不同：

  - 每层都是从0开始搜索而不是startIndex
  - 需要used数组记录path里都放了哪些元素了

代码：

- 需要对这题的used和上提的used看一下，为什么这里要改为False，为什么上一题不需要

![image-20220420150529264](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220420150529264.png)

#### [47. 全排列 II](https://leetcode-cn.com/problems/permutations-ii/)

难度中等1021

给定一个可包含重复数字的序列 `nums` ，***按任意顺序*** 返回所有不重复的全排列。

 

**示例 1：**

```
输入：nums = [1,1,2]
输出：
[[1,1,2],
 [1,2,1],
 [2,1,1]]
```

**示例 2：**

```
输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

 

**提示：**

- `1 <= nums.length <= 8`
- `-10 <= nums[i] <= 10`



思路：

- 和上一题的区别在于可能包含重复的items

- 如果nums都不重复，结果将和上一题一样

- 在[40.组合总和II (opens new window)](https://programmercarl.com/0040.组合总和II.html)、[90.子集II (opens new window)](https://programmercarl.com/0090.子集II.html)我们分别详细讲解了组合问题和子集问题如何去重。

  那么排列问题其实也是一样的套路。

  **还要强调的是去重一定要对元素进行排序，这样我们才方便通过相邻的节点来判断是否重复使用了**。

  我以示例中的 [1,1,2]为例 （为了方便举例，已经排序）抽象为一棵树，去重过程如图：

  ![47.全排列II1](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20201124201331223.png)

- 可以看到同一树层不能存在重复的值，同一树枝可以存在重复的值

- 总结一下：**一般来说：组合问题和排列问题是在树形结构的叶子节点上收集结果，而子集问题就是取树上所有节点的结果**。

代码：

![image-20220420214402048](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220420214402048.png)

- 子集问题分析：

  - 时间复杂度：$O(n × 2^n)$，因为每一个元素的状态无外乎取与不取，所以时间复杂度为$O(2^n)$，构造每一组子集都需要填进数组，又有需要$O(n)$，最终时间复杂度：$O(n × 2^n)$。
  - 空间复杂度：$O(n)$，递归深度为n，所以系统栈所用空间为$O(n)$，每一层递归所用的空间都是常数级别，注意代码里的result和path都是全局变量，就算是放在参数里，传的也是引用，并不会新申请内存空间，最终空间复杂度为$O(n)$。

  排列问题分析：

  - 时间复杂度：$O(n!)$，这个可以从排列的树形图中很明显发现，每一层节点为n，第二层每一个分支都延伸了n-1个分支，再往下又是n-2个分支，所以一直到叶子节点一共就是 n * n-1 * n-2 * ..... 1 = n!。
  - 空间复杂度：$O(n)$，和子集问题同理。

  组合问题分析：

  - 时间复杂度：$O(n × 2^n)$，组合问题其实就是一种子集的问题，所以组合问题最坏的情况，也不会超过子集问题的时间复杂度。
  - 空间复杂度：$O(n)$，和子集问题同理。

  **一般说道回溯算法的复杂度，都说是指数级别的时间复杂度，这也算是一个概括吧！**

#### [332. Reconstruct Itinerary](https://leetcode-cn.com/problems/reconstruct-itinerary/)

难度困难552

You are given a list of airline `tickets` where `tickets[i] = [fromi, toi]` represent the departure and the arrival airports of one flight. Reconstruct the itinerary in order and return it.

All of the tickets belong to a man who departs from `"JFK"`, thus, the itinerary must begin with `"JFK"`. If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string.

- For example, the itinerary `["JFK", "LGA"]` has a smaller lexical order than `["JFK", "LGB"]`.

You may assume all tickets form at least one valid itinerary. You must use all the tickets once and only once.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/14/itinerary1-graph.jpg)

```
Input: tickets = [["MUC","LHR"],["JFK","MUC"],["SFO","SJC"],["LHR","SFO"]]
Output: ["JFK","MUC","LHR","SFO","SJC"]
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/itinerary2-graph.jpg)

```
Input: tickets = [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
Output: ["JFK","ATL","JFK","SFO","ATL","SFO"]
Explanation: Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"] but it is larger in lexical order.
```

 

**Constraints:**

- `1 <= tickets.length <= 300`
- `tickets[i].length == 2`
- `fromi.length == 3`
- `toi.length == 3`
- `fromi` and `toi` consist of uppercase English letters.
- `fromi != toi`



思路：

- 直觉上来看 这道题和回溯法没有什么关系，更像是图论中的深度优先搜索。

  实际上确实是深搜，但这是深搜中使用了回溯的例子，在查找路径的时候，如果不回溯，怎么能查到目标路径呢。

  所以我倾向于说本题应该使用回溯法，那么我也用回溯法的思路来讲解本题，其实深搜一般都使用了回溯法的思路

- **这道题目有几个难点：**

  1. 一个行程中，如果航班处理不好容易变成一个圈，成为死循环
  2. 有多种解法，字母序靠前排在前面，让很多同学望而退步，如何该记录映射关系呢 ？
  3. 使用回溯法（也可以说深搜） 的话，那么终止条件是什么呢？
  4. 搜索的过程中，如何遍历一个机场所对应的所有机场。

- 对于死循环：

  <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20201115180537865.png" alt="332.重新安排行程" style="zoom:50%;" />

  - 本题以输入：[["JFK", "KUL"], ["JFK", "NRT"], ["NRT", "JFK"]为例，抽象为树形结构如下：
  - <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/2020111518065555.png" alt="332.重新安排行程1" style="zoom:50%;" />
  - 递归终止条件：
  - 输入: [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]] ，这是有4个航班，那么只要找出一种行程，行程里的机场个数是5就可以了。
  - 所以终止条件是：我们回溯遍历的过程中，遇到的机场个数，如果达到了（航班数量+1），那么我们就找到了一个行程，把所有航班串在一起了

代码：

![image-20220421125949015](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421125949015.png)

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

思路：

首先来看一下皇后们的约束条件：

1. 不能同行
2. 不能同列
3. 不能同斜线

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20210130182532303.jpg" alt="51.N皇后" style="zoom:50%;" />

**只要搜索到了树的叶子节点，说明就找到了皇后们的合理位置了**

- 递归函数参数:

  定义全局变量二维数组result_list来记录最终结果。

  参数n是棋盘的大小，然后用row来记录当前遍历到棋盘的第几层了

- 终止条件：

  可以看出，当递归到棋盘最底层（也就是叶子节点）的时候，就可以收集结果并返回了

- 验证棋盘是否合法

  - 不能同行
  - 不能同列
  - 不能同斜线 （45度和135度角）



代码：

#### [37. 解数独](https://leetcode-cn.com/problems/sudoku-solver/)

难度困难1212

编写一个程序，通过填充空格来解决数独问题。

数独的解法需 **遵循如下规则**：

1. 数字 `1-9` 在每一行只能出现一次。
2. 数字 `1-9` 在每一列只能出现一次。
3. 数字 `1-9` 在每一个以粗实线分隔的 `3x3` 宫内只能出现一次。（请参考示例图）

数独部分空格内已填入了数字，空白格用 `'.'` 表示。

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/250px-sudoku-by-l2g-20050714svg.png)

```
输入：board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
输出：[["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
解释：输入的数独如上图所示，唯一有效的解决方案如下所示：
```

 

**提示：**

- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` 是一位数字或者 `'.'`
- 题目数据 **保证** 输入数独仅有一个解



思路：



代码：





#### [784. 字母大小写全排列](https://leetcode-cn.com/problems/letter-case-permutation/)

难度中等373

给定一个字符串 `s` ，通过将字符串 `s` 中的每个字母转变大小写，我们可以获得一个新的字符串。

返回 *所有可能得到的字符串集合* 。以 **任意顺序** 返回输出。

 

**示例 1：**

```
输入：s = "a1b2"
输出：["a1b2", "a1B2", "A1b2", "A1B2"]
```

**示例 2:**

```
输入: s = "3z4"
输出: ["3z4","3Z4"]
```

 

**提示:**

- `1 <= s.length <= 12`
- `s` 由小写英文字母、大写英文字母和数字组成

#### [面试题 08.09. 括号](https://leetcode-cn.com/problems/bracket-lcci/) & [22. 括号生成](https://leetcode-cn.com/problems/generate-parentheses/) & [剑指 Offer II 085. 生成匹配的括号](https://leetcode-cn.com/problems/IDBivT/)

难度中等110

括号。设计一种算法，打印n对括号的所有合法的（例如，开闭一一对应）组合。

说明：解集不能包含重复的子集。

例如，给出 n = 3，生成结果为：

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```





#### [401. Binary Watch](https://leetcode-cn.com/problems/binary-watch/)

难度简单356

A binary watch has 4 LEDs on the top which represent the hours (0-11), and the 6 LEDs on the bottom represent the minutes (0-59). Each LED represents a zero or one, with the least significant bit on the right.

- For example, the below binary watch reads `"4:51"`.

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/binarywatch.jpg)

Given an integer `turnedOn` which represents the number of LEDs that are currently on, return *all possible times the watch could represent*. You may return the answer in **any order**.

The hour must not contain a leading zero.

- For example, `"01:00"` is not valid. It should be `"1:00"`.

The minute must be consist of two digits and may contain a leading zero.

- For example, `"10:2"` is not valid. It should be `"10:02"`.

 

**Example 1:**

```
Input: turnedOn = 1
Output: ["0:01","0:02","0:04","0:08","0:16","0:32","1:00","2:00","4:00","8:00"]
```

**Example 2:**

```
Input: turnedOn = 9
Output: []
```

 

**Constraints:**

- `0 <= turnedOn <= 10`

#### [257. Binary Tree Paths](https://leetcode-cn.com/problems/binary-tree-paths/)

难度简单714

Given the `root` of a binary tree, return *all root-to-leaf paths in **any order***.

A **leaf** is a node with no children.

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/paths-tree.jpg)

```
Input: root = [1,2,3,null,5]
Output: ["1->2->5","1->3"]
```

**Example 2:**

```
Input: root = [1]
Output: ["1"]
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[1, 100]`.
- `-100 <= Node.val <= 100`







