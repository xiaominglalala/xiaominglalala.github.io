主要参考leetcode的书

### 1.1 深度优先遍历使用的数据结构（栈）：

在深度优先遍历的过程中，需要将 当前遍历到的结点 的相邻结点 暂时保存 起来，以便在回退的时候可以继续访问它们。遍历到的结点的顺序呈现「后进先出」的特点，因此 深度优先遍历可以通过「栈」实现。

在Python中，列表就满足后进先出的要求（append，pop）

对于之前做过的二叉树的前中后序遍历，使用recursion（递归）是很容易想到的，但是使用iteration是比较难的，也是可能会被作为follow up的考点。推荐DFS都使用recursion来实现

![image-20220417084221574](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417084221574.png)

主要是掌握前中后序的迭代和递归写法

### 1.2 广度优先遍历使用的数据结构（队列）：

### 1.3 树的深度优先搜索：

- 「根结点 → 右子树 → 左子树」
- ![image-20220416234821547](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220416234821547.png)
- 前序（preorder）遍历：<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220416235111780.png" alt="image-20220416235111780" style="zoom: 67%;" />
- 中序(Inorder)遍历
- <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220416235225435.png" alt="image-20220416235225435" style="zoom:67%;" />
- 后序(Posorder)遍历
- <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417085922348.png" alt="image-20220417085922348" style="zoom:67%;" />

> 后序遍历最为重要

#### Preorder Binary Tree (Iteration)

- 前序遍历是中左右；
- <img src="https://pic.leetcode-cn.com/6233a9685447d0b4d7b513f739151ca065e5697e24070bcafc1ee5d28f9155a6.png" alt="中序遍历流程图" style="zoom: 33%;" />
- ![image-20220417100825910](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417100825910.png)

#### Preorder Binary Tree (Recursion)

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220217135851527.png" alt="image-20220217135851527" style="zoom: 67%;" />

#### Postorder Binary Tree (Iteration)

- 对于后序遍历的迭代法，就基本改一下前序遍历中的内容即可
- 前序遍历是中左右，后序遍历是左右中
- 那么我们只需要压入左右时和前序换一下，先压入左再压入右
- 最后反转数组

![image-20220417102432062](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417102432062.png)

注意不可以return list.reverse()

![image-20220417102509035](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417102509035.png)

#### Postorder Binary Tree (Recursion)

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417102542959.png" alt="image-20220417102542959" style="zoom:50%;" />

#### Inorder Binary Tree (Iteration)

- 前序遍历的顺序是中左右, 而对于一个binary tree, 先访问的元素是中间节点，要处理的元素也是中间节点。**前序要访问的元素和要处理的元素顺序是一致的，都是中间节点。**
- 中序遍历的顺序是左中右，先访问的是二叉树顶部的节点，然后一层一层向下访问，直到到达树左面的最底部，再开始处理节点（也就是在把节点的数值放进result数组中）就造成了**处理顺序和访问顺序是不一致的。**
- **使用迭代法写中序遍历，就需要借用指针的遍历来帮助访问节点，栈则用来处理节点上的元素。**

![image-20220417103649282](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417103649282.png)



#### Inorder Binary Tree (Recursion)

<img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220217142708700.png" alt="image-20220217142708700" style="zoom: 67%;" />

> 之后再考虑下N叉树的iteration

### 



### 1.4 图的深度优先搜索：

深度优先遍历有「回头」的过程，在树中由于不存在「环」（回路），对于每一个结点来说，每一个结点只会被递归处理一次。而「图」中由于存在「环」（回路），就需要 记录已经被递归处理的结点（通常使用布尔数组或者哈希表），以免结点被重复遍历到。

### 1.5 树的广度优先遍历：

- 树的广度优先遍历的写法模式相对固定：
  - 使用队列；
  - 在队列非空的时候，动态取出队首元素；
  - 取出队首元素的时候，把队首元素相邻的结点（非空）加入队列。

比如对于102题的二叉树层序遍历：

二叉树：`[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

<img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220217174904929.png" alt="image-20220217174904929" style="zoom:67%;" />



### 1.6 图的广度优先遍历：

- 在 无权图 中，由于广度优先遍历本身的特点，假设源点为 source，只有在遍历到 所有 距离源点 source 的距离为 d 的所有结点以后，才能遍历到所有 距离源点 source 的距离为 d + 1 的所有结点。也可以使用「两点之间、线段最短」这条经验来辅助理解如下结论：从源点 source 到目标结点 target 走直线走过的路径一定是最短的。

- 和深度优先遍历一样，广度优先遍历也需要在遍历的时候记录已经遍历过的结点。

- 特别注意：将结点添加到队列以后，一定要马上标记为「已经访问」，否则相同结点会重复入队，这一点在初学的时候很容易忽略。如果很难理解这样做的必要性，建议大家在代码中打印出队列中的元素进行调试：在图中，如果入队的时候不马上标记为「已访问」，相同的结点会重复入队

- 广度优先遍历用于求解「无权图」的最短路径，因此一定要认清「无权图」这个前提条件。如果是带权图，就需要使用相应的专门的算法去解决它们。事实上，这些「专门」的算法的思想也都基于「广度优先遍历」的思想

  - 带权有向图、且所有权重都非负的单源最短路径问题：使用 Dijkstra 算法；
  - 带权有向图的单源最短路径问题：Bellman-Ford 算法；
  - 一个图的所有结点对的最短路径问题：Floy-Warshall 算法。

- 应用任何一种算法，都需要认清使用算法的前提，不满足前提直接套用算法是不可取的。深刻理解应用算法的前提，也是学习算法的重要方法。例如我们在学习「二分查找」算法、「滑动窗口」算法的时候，就可以问自己，这个问题为什么可以使用「二分查找」，为什么可以使用「滑动窗口」。我们知道一个问题可以使用「优先队列」解决，是什么样的需求促使我们想到使用「优先队列」，而不是「红黑树（平衡二叉搜索树）」，想清楚使用算法（数据结构）的前提更重要。


#### [323. Number of Connected Components in an Undirected Graph](https://leetcode-cn.com/problems/number-of-connected-components-in-an-undirected-graph/)

难度中等131

You have a graph of `n` nodes. You are given an integer `n` and an array `edges` where `edges[i] = [ai, bi]` indicates that there is an edge between `ai` and `bi` in the graph.

Return *the number of connected components in the graph*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/14/conn1-graph.jpg)

```
Input: n = 5, edges = [[0,1],[1,2],[3,4]]
Output: 2
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/03/14/conn2-graph.jpg)

```
Input: n = 5, edges = [[0,1],[1,2],[2,3],[3,4]]
Output: 1
```

 

**Constraints:**

- `1 <= n <= 2000`
- `1 <= edges.length <= 5000`
- `edges[i].length == 2`
- `0 <= ai <= bi < n`
- `ai != bi`
- There are no repeated edges.

思路：

- 首先需要对输入数组进行处理，由于 n 个结点的编号从 0 到 n - 1 ，因此可以使用「嵌套数组」表示邻接表
  然后遍历每一个顶点，对每一个顶点执行一次广度优先遍历，注意：在遍历的过程中使用 visited 布尔数组记录已经遍历过的结点。
- 注意defaultdict(list)维护的dict用list作为值
  - ![image-20220417141036582](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417141036582.png)
- 这个部分会不断递归<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417141206072.png" alt="image-20220417141206072" style="zoom:50%;" />
  - 比如我们一开始看到的que是[0]， 在popleft了0后, 它在搜索后发现1是连着的，就会加上1，变成[1]; 
  - 再popleft了1后发现2是连着的，就会加上2，变成2。
  - 2会看2连什么，2连的是1，1已经visited了，所以就没了，但是这时候visited是[0,1,2]
  - 然后回到第一的函数，找每visited的点

代码：

![image-20220417130857404](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417130857404.png)

![image-20220417133152089](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417133152089.png)



- 广度优先遍历可以用于「树」和「图」的问题的遍历；
- 广度优先遍历作用于「无权图」，得到的是「最短路径」。如果题目有让求「最小」、「最短」、「最少」，可以考虑这个问题是不是可以建立成一个「图形结构」或者「树形结构」，用「广度优先遍历」的思想求得「最小」、「最短」、「最少」的数值；
- 广度优先遍历作用于图论问题的时候，结点在加入队列以后标记为已经访问，否则会出现结点重复入队的情况。

### 1.7 回溯算法

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

### 1.8 二维平面的搜索问题（Flood Fill）

![image.png](https://pic.leetcode-cn.com/1611489764-dXtjvl-image.png)

#### [79. Word Search](https://leetcode-cn.com/problems/word-search/)

难度中等1259

Given an `m x n` grid of characters `board` and a string `word`, return `true` *if* `word` *exists in the grid*.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/word-1.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true
```

**Example 3:**

![img](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
```

 

**Constraints:**

- `m == board.length`
- `n = board[i].length`
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board` and `word` consists of only lowercase and uppercase English letters.

 

**Follow up:** Could you use search pruning to make your solution faster with a larger `board`?

思路：



代码：



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



### 1.9 抽象成图论问题

抽象成图论问题
在算法面试和笔试中，有一些问题问我们「最短」、「最少」、「最小」，可以尝试将它们转换为求解无权图的最短路径的问题求解。

对于这一类问题，最重要的一点在于分析出这一类问题的「图」结构，也就是对图形问题建模。依然是要注意到这些问题的背后是一个「无权图」的最短路径问题，因此可以使用「广度优先遍历」。



### 1.10 深度优先遍历的应用：

在一些树的问题中，其实就是通过一次深度优先遍历，获得树的某些属性。例如：「二叉树」的最大深度、「二叉树」的最小深度、平衡二叉树、是否 BST。在遍历的过程中，通常需要设计一些变量，一边遍历，一边更新设计的变量的值

#### [129. Sum Root to Leaf Numbers](https://leetcode-cn.com/problems/sum-root-to-leaf-numbers/)

难度中等511

You are given the `root` of a binary tree containing digits from `0` to `9` only.

Each root-to-leaf path in the tree represents a number.

- For example, the root-to-leaf path `1 -> 2 -> 3` represents the number `123`.

Return *the total sum of all root-to-leaf numbers*. Test cases are generated so that the answer will fit in a **32-bit** integer.

A **leaf** node is a node with no children.

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/num1tree.jpg)

```
Input: root = [1,2,3]
Output: 25
Explanation:
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/02/19/num2tree.jpg)

```
Input: root = [4,9,0,5,1]
Output: 1026
Explanation:
The root-to-leaf path 4->9->5 represents the number 495.
The root-to-leaf path 4->9->1 represents the number 491.
The root-to-leaf path 4->0 represents the number 40.
Therefore, sum = 495 + 491 + 40 = 1026.
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[1, 1000]`.
- `0 <= Node.val <= 9`
- The depth of the tree will not exceed `10`.

思路：

- 思路上使用DFS是很自然的：从根部开始，每次遇到结点，就把之前的数值*10再加上节点的值。
  - 如果遇到叶子节点，就把计算出来的值加到result里面
  - 如果不是叶子节点，则递归遍历
- 如果使用BFS，需要维护两个队列，分别存储节点和数值

### 1.11 拓扑排序

#### [1136. Parallel Courses](https://leetcode-cn.com/problems/parallel-courses/)

难度中等46

You are given an integer `n`, which indicates that there are `n` courses labeled from `1` to `n`. You are also given an array `relations` where `relations[i] = [prevCoursei, nextCoursei]`, representing a prerequisite relationship between course `prevCoursei` and course `nextCoursei`: course `prevCoursei` has to be taken before course `nextCoursei`.

In one semester, you can take **any number** of courses as long as you have taken all the prerequisites in the **previous** semester for the courses you are taking.

Return *the **minimum** number of semesters needed to take all courses*. If there is no way to take all the courses, return `-1`.

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/course1graph.jpg)

```
Input: n = 3, relations = [[1,3],[2,3]]
Output: 2
Explanation: The figure above represents the given graph.
In the first semester, you can take courses 1 and 2.
In the second semester, you can take course 3.
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/course2graph.jpg)

```
Input: n = 3, relations = [[1,2],[2,3],[3,1]]
Output: -1
Explanation: No course can be studied because they are prerequisites of each other.
```

 

**Constraints:**

- `1 <= n <= 5000`
- `1 <= relations.length <= 5000`
- `relations[i].length == 2`
- `1 <= prevCoursei, nextCoursei <= n`
- `prevCoursei != nextCoursei`
- All the pairs `[prevCoursei, nextCoursei]` are **unique**.

#### [207. Course Schedule](https://leetcode-cn.com/problems/course-schedule/)

难度中等1231

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

- For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

 

**Example 1:**

```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
```

**Example 2:**

```
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
```

 

**Constraints:**

- `1 <= numCourses <= 105`
- `0 <= prerequisites.length <= 5000`
- `prerequisites[i].length == 2`
- `0 <= ai, bi < numCourses`
- All the pairs prerequisites[i] are **unique**.

通过次数197,923

提交次数367,451

#### [269. Alien Dictionary](https://leetcode-cn.com/problems/alien-dictionary/) & [剑指 Offer II 114. 外星文字典](https://leetcode-cn.com/problems/Jf1JuT/)

难度困难218

There is a new alien language that uses the English alphabet. However, the order among the letters is unknown to you.

You are given a list of strings `words` from the alien language's dictionary, where the strings in `words` are **sorted lexicographically** by the rules of this new language.

Return *a string of the unique letters in the new alien language sorted in **lexicographically increasing order** by the new language's rules. If there is no solution, return* `""`*. If there are multiple solutions, return **any of them***.

A string `s` is **lexicographically smaller** than a string `t` if at the first letter where they differ, the letter in `s` comes before the letter in `t` in the alien language. If the first `min(s.length, t.length)` letters are the same, then `s` is smaller if and only if `s.length < t.length`.

 

**Example 1:**

```
Input: words = ["wrt","wrf","er","ett","rftt"]
Output: "wertf"
```

**Example 2:**

```
Input: words = ["z","x"]
Output: "zx"
```

**Example 3:**

```
Input: words = ["z","x","z"]
Output: ""
Explanation: The order is invalid, so return "".
```

 

**Constraints:**

- `1 <= words.length <= 100`
- `1 <= words[i].length <= 100`
- `words[i]` consists of only lowercase English letters.



#### [210. Course Schedule II](https://leetcode-cn.com/problems/course-schedule-ii/)

难度中等609

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

- For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return *the ordering of courses you should take to finish all courses*. If there are many valid answers, return **any** of them. If it is impossible to finish all courses, return **an empty array**.

 

**Example 1:**

```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1].
```

**Example 2:**

```
Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
Output: [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].
```

**Example 3:**

```
Input: numCourses = 1, prerequisites = []
Output: [0]
```

 

**Constraints:**

- `1 <= numCourses <= 2000`
- `0 <= prerequisites.length <= numCourses * (numCourses - 1)`
- `prerequisites[i].length == 2`
- `0 <= ai, bi < numCourses`
- `ai != bi`
- All the pairs `[ai, bi]` are **distinct**.

#### [630. Course Schedule III](https://leetcode-cn.com/problems/course-schedule-iii/)

难度困难327

There are `n` different online courses numbered from `1` to `n`. You are given an array `courses` where `courses[i] = [durationi, lastDayi]` indicate that the `ith` course should be taken **continuously** for `durationi` days and must be finished before or on `lastDayi`.

You will start on the `1st` day and you cannot take two or more courses simultaneously.

Return *the maximum number of courses that you can take*.

 

**Example 1:**

```
Input: courses = [[100,200],[200,1300],[1000,1250],[2000,3200]]
Output: 3
Explanation: 
There are totally 4 courses, but you can take 3 courses at most:
First, take the 1st course, it costs 100 days so you will finish it on the 100th day, and ready to take the next course on the 101st day.
Second, take the 3rd course, it costs 1000 days so you will finish it on the 1100th day, and ready to take the next course on the 1101st day. 
Third, take the 2nd course, it costs 200 days so you will finish it on the 1300th day. 
The 4th course cannot be taken now, since you will finish it on the 3300th day, which exceeds the closed date.
```

**Example 2:**

```
Input: courses = [[1,2]]
Output: 1
```

**Example 3:**

```
Input: courses = [[3,2],[4,3]]
Output: 0
```

 

**Constraints:**

- `1 <= courses.length <= 104`
- `1 <= durationi, lastDayi <= 104`

#### [261. Graph Valid Tree](https://leetcode-cn.com/problems/graph-valid-tree/)

难度中等165

You have a graph of `n` nodes labeled from `0` to `n - 1`. You are given an integer n and a list of `edges` where `edges[i] = [ai, bi]` indicates that there is an undirected edge between nodes `ai` and `bi` in the graph.

Return `true` *if the edges of the given graph make up a valid tree, and* `false` *otherwise*.

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/tree1-graph.jpg)

```
Input: n = 5, edges = [[0,1],[0,2],[0,3],[1,4]]
Output: true
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/tree2-graph.jpg)

```
Input: n = 5, edges = [[0,1],[1,2],[2,3],[1,3],[1,4]]
Output: false
```

 

**Constraints:**

- `1 <= n <= 2000`
- `0 <= edges.length <= 5000`
- `edges[i].length == 2`
- `0 <= ai, bi < n`
- `ai != bi`
- There are no self-loops or repeated edges.

#### [310. Minimum Height Trees](https://leetcode-cn.com/problems/minimum-height-trees/)

难度中等636

A tree is an undirected graph in which any two vertices are connected by *exactly* one path. In other words, any connected graph without simple cycles is a tree.

Given a tree of `n` nodes labelled from `0` to `n - 1`, and an array of `n - 1` `edges` where `edges[i] = [ai, bi]` indicates that there is an undirected edge between the two nodes `ai` and `bi` in the tree, you can choose any node of the tree as the root. When you select a node `x` as the root, the result tree has height `h`. Among all possible rooted trees, those with minimum height (i.e. `min(h)`) are called **minimum height trees** (MHTs).

Return *a list of all **MHTs'** root labels*. You can return the answer in **any order**.

The **height** of a rooted tree is the number of edges on the longest downward path between the root and a leaf.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/09/01/e1.jpg)

```
Input: n = 4, edges = [[1,0],[1,2],[1,3]]
Output: [1]
Explanation: As shown, the height of the tree is 1 when the root is the node with label 1 which is the only MHT.
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/e2.jpg)

```
Input: n = 6, edges = [[3,0],[3,1],[3,2],[3,4],[5,4]]
Output: [3,4]
```

 

**Constraints:**

- `1 <= n <= 2 * 104`
- `edges.length == n - 1`
- `0 <= ai, bi < n`
- `ai != bi`
- All the pairs `(ai, bi)` are distinct.
- The given input is **guaranteed** to be a tree and there will be **no repeated** edges.

#### [886. Possible Bipartition](https://leetcode-cn.com/problems/possible-bipartition/)

难度中等168

We want to split a group of `n` people (labeled from `1` to `n`) into two groups of **any size**. Each person may dislike some other people, and they should not go into the same group.

Given the integer `n` and the array `dislikes` where `dislikes[i] = [ai, bi]` indicates that the person labeled `ai` does not like the person labeled `bi`, return `true` *if it is possible to split everyone into two groups in this way*.

 

**Example 1:**

```
Input: n = 4, dislikes = [[1,2],[1,3],[2,4]]
Output: true
Explanation: group1 [1,4] and group2 [2,3].
```

**Example 2:**

```
Input: n = 3, dislikes = [[1,2],[1,3],[2,3]]
Output: false
```

**Example 3:**

```
Input: n = 5, dislikes = [[1,2],[2,3],[3,4],[4,5],[1,5]]
Output: false
```

 

**Constraints:**

- `1 <= n <= 2000`
- `0 <= dislikes.length <= 104`
- `dislikes[i].length == 2`
- `1 <= dislikes[i][j] <= n`
- `ai < bi`
- All the pairs of `dislikes` are **unique**.

- 

#### [1245. Tree Diameter](https://leetcode-cn.com/problems/tree-diameter/)

难度中等90

The **diameter** of a tree is **the number of edges** in the longest path in that tree.

There is an undirected tree of `n` nodes labeled from `0` to `n - 1`. You are given a 2D array `edges` where `edges.length == n - 1` and `edges[i] = [ai, bi]` indicates that there is an undirected edge between nodes `ai` and `bi` in the tree.

Return *the **diameter** of the tree*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2022/01/19/tree1.jpg)

```
Input: edges = [[0,1],[0,2]]
Output: 2
Explanation: The longest path of the tree is the path 1 - 0 - 2.
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/tree2.jpg)

```
Input: edges = [[0,1],[1,2],[2,3],[1,4],[4,5]]
Output: 4
Explanation: The longest path of the tree is the path 3 - 2 - 1 - 4 - 5.
```

 

**Constraints:**

- `n == edges.length + 1`
- `1 <= n <= 104`
- `0 <= ai, bi < n`
- `ai != bi`

### 1.12 双向BFS和多源BFS

### 1.13 动态规划和深度优先遍历的结合

代码：

回溯搜索是深度优先搜索（DFS）的一种，回溯法通俗的将其采用的思想是“一直向下走，走不通就掉头”，类似于树的先序遍历。dfs和回溯法其主要的区别是：回溯法在求解过程中不保留完整的树结构，而深度优先搜索则记下完整的搜索树。
  为了减少存储空间，在深度优先搜索中，用标志的方法记录访问过的状态，这种处理方法使得深度优先搜索法与回溯法没什么区别了。
由于回溯法花费时间较长，所以对于没有明确的动态规划（DP）和递归解法的或问题要求满足某种性质（约束条件）的所有解或最优解时，才考虑使用回溯法。

  我们一般在求解**八皇后问题**的时候说使用的是回溯法，本质也是深搜。在求解有关树和图的问题时，习惯说成**深度优先搜索**。这里所说的回溯和深搜都是不做任何优化的方式实现，在全局解空间上寻找最优解，所花费的时间比较长，仅使用于数据规模较小的问题。



### 1.14 Union Find 专题

#### Part 1. 基本概念

- 并查集是一种数据结构
- 并查集这三个字，一个字代表一个意思。
- 并（Union），代表合并
- 查（Find），代表查找
- 集（Set），代表这是一个以字典为基础的数据结构，它的基本功能是合并集合中的元素，查找集合中的元素
- 并查集的典型应用是有关连通分量的问题
- 并查集解决单个问题（添加，合并，查找）的时间复杂度都是O(1)
- 因此，并查集可以应用到在线算法中

#### Part 2. Union Find的实现

- 数据结构
  - 并查集跟树有些类似，只不过她跟树是相反的。在树这个数据结构里面，每个节点会记录它的子节点。在并查集里，每个节点会记录它的父节
  - ![image-20220421173045861](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421173045861.png)
  - <img src="https://pic.leetcode-cn.com/1609980000-ofFjdW-幻灯片1.JPG" alt="幻灯片1.JPG" style="zoom:50%;" />
  - 如果节点是相互连通的（从一个节点可以到达另一个节点），那么他们在同一棵树里，或者说在同一个集合里，或者说他们的**祖先是相同的**。
- 初始化：
  - 当把一个新节点添加到并查集中，它的父节点应该为空![image-20220421173335822](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421173335822.png)
  - <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421173355463.png" alt="image-20220421173355463" style="zoom:50%;" />

- 合并节点:
  - 如果发现两个节点是连通的，那么就要把他们合并，也就是他们的祖先是相同的。这里究竟把谁当做父节点一般是没有区别的。
  - ![image-20220421173615698](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421173615698.png)
  - <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421173551977.png" alt="image-20220421173551977" style="zoom:50%;" />

- 两节点是否连通
  - 我们判断两个节点是否处于同一个连通分量的时候，就需要判断它们的祖先是否相同
  - ![image-20220421173713692](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421173713692.png)

- 查找祖先
  - 查找祖先的方法是：如果节点的父节点不为空，那就不断迭代
  - ![image-20220421173741018](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421173741018.png)
  - 这里有一个优化的点：如果我们树很深，比如说退化成链表，那么每次查询的效率都会非常低。所以我们要做一下路径压缩。也就是把树的深度固定为二。这么做可行的原因是，并查集只是记录了节点之间的连通关系，而节点相互连通只需要有一个相同的祖先就可以了。
  - <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421174025892.png" alt="image-20220421174025892" style="zoom:67%;" />
  - <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421173938999.png" alt="image-20220421173919553" style="zoom: 67%;" />
  - ![image-20220421174047065](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421174047065.png)
  - ![image-20220421174107828](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421174107828.png)

- 完整模板
  - ![image-20220421174643330](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421174643330.png)


上述的模板是无权的，加上权重以后，在原模板上添加几行即可。

#### [990. Satisfiability of Equality Equations](https://leetcode-cn.com/problems/satisfiability-of-equality-equations/)

难度中等230

You are given an array of strings `equations` that represent relationships between variables where each string `equations[i]` is of length `4` and takes one of two different forms: `"xi==yi"` or `"xi!=yi"`.Here, `xi` and `yi` are lowercase letters (not necessarily different) that represent one-letter variable names.

Return `true` *if it is possible to assign integers to variable names so as to satisfy all the given equations, or* `false` *otherwise*.

 

**Example 1:**

```
Input: equations = ["a==b","b!=a"]
Output: false
Explanation: If we assign say, a = 1 and b = 1, then the first equation is satisfied, but not the second.
There is no way to assign the variables to satisfy both equations.
```

**Example 2:**

```
Input: equations = ["b==a","a==b"]
Output: true
Explanation: We could assign a = 1 and b = 1 to satisfy both equations.
```

 

**Constraints:**

- `1 <= equations.length <= 500`
- `equations[i].length == 4`
- `equations[i][0]` is a lowercase letter.
- `equations[i][1]` is either `'='` or `'!'`.
- `equations[i][2]` is `'='`.
- `equations[i][3]` is a lowercase letter.

思路：

- 并查集分为两部分：

  - 合并
    两棵树合并，即：把【其中一颗树的根节点】的【父节点】，置为【另一颗树的根节点】
  - 查询
    根节点：父节点是它的本身
    其他：递归查询它的父节点
  
- 主函数

  - 构建包含所有相等元素的图
    针对包含【!=】的式子，查询两端的字母是否包含在同一个集合中（即：根节点相同）

  

代码：

![image-20220421205913446](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421205913446.png)

#### [399. Evaluate Division](https://leetcode-cn.com/problems/evaluate-division/)

难度中等727

You are given an array of variable pairs `equations` and an array of real numbers `values`, where `equations[i] = [Ai, Bi]` and `values[i]` represent the equation `Ai / Bi = values[i]`. Each `Ai` or `Bi` is a string that represents a single variable.

You are also given some `queries`, where `queries[j] = [Cj, Dj]` represents the `jth` query where you must find the answer for `Cj / Dj = ?`.

Return *the answers to all queries*. If a single answer cannot be determined, return `-1.0`.

**Note:** The input is always valid. You may assume that evaluating the queries will not result in division by zero and that there is no contradiction.

 

**Example 1:**

```
Input: equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
Output: [6.00000,0.50000,-1.00000,1.00000,-1.00000]
Explanation: 
Given: a / b = 2.0, b / c = 3.0
queries are: a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ?
return: [6.0, 0.5, -1.0, 1.0, -1.0 ]
```

**Example 2:**

```
Input: equations = [["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = [["a","c"],["c","b"],["bc","cd"],["cd","bc"]]
Output: [3.75000,0.40000,5.00000,0.20000]
```

**Example 3:**

```
Input: equations = [["a","b"]], values = [0.5], queries = [["a","b"],["b","a"],["a","c"],["x","y"]]
Output: [0.50000,2.00000,-1.00000,-1.00000]
```

 

**Constraints:**

- `1 <= equations.length <= 20`
- `equations[i].length == 2`
- `1 <= Ai.length, Bi.length <= 5`
- `values.length == equations.length`
- `0.0 < values[i] <= 20.0`
- `1 <= queries.length <= 20`
- `queries[i].length == 2`
- `1 <= Cj.length, Dj.length <= 5`
- `Ai, Bi, Cj, Dj` consist of lower case English letters and digits.

思路：

- <img src="https://pic.leetcode-cn.com/1609860627-dZoDYx-image.png" alt="img" style="zoom:50%;" />

- 如何在「find查询」操作的「路径压缩」优化中维护权值变化

- ![image.png](https://pic.leetcode-cn.com/1609861645-DbxMDs-image.png)

- 如何在「合并」操作中维护权值的变化。

- 合并」操作基于这样一个 很重要的前提：我们将要合并的两棵树的高度最多为 2，换句话说两棵树都必需是「路径压缩」以后的效果，两棵树的叶子结点到根结点最多只需要经过一条有向边。

- ![image-20220421210710678](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421210710678.png)

- ![image-20220421211411623](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421211411623.png)

- 

- 

  

## 深度优先搜索





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



#### [212. Word Search II](https://leetcode-cn.com/problems/word-search-ii/)

难度困难641

Given an `m x n` `board` of characters and a list of strings `words`, return *all words on the board*.

Each word must be constructed from letters of sequentially adjacent cells, where **adjacent cells** are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/07/search1.jpg)

```
Input: board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/search2.jpg)

```
Input: board = [["a","b"],["c","d"]], words = ["abcb"]
Output: []
```

 

**Constraints:**

- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 12`
- `board[i][j]` is a lowercase English letter.
- `1 <= words.length <= 3 * 104`
- `1 <= words[i].length <= 10`
- `words[i]` consists of lowercase English letters.
- All the strings of `words` are unique.

#### [297. 二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)

难度困难822

序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。

请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

**提示:** 输入输出格式与 LeetCode 目前使用的方式一致，详情请参阅 [LeetCode 序列化二叉树的格式](https://leetcode-cn.com/faq/#binary-tree)。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/serdeser.jpg)

```
输入：root = [1,2,3,null,null,4,5]
输出：[1,2,3,null,null,4,5]
```

**示例 2：**

```
输入：root = []
输出：[]
```

**示例 3：**

```
输入：root = [1]
输出：[1]
```

**示例 4：**

```
输入：root = [1,2]
输出：[1,2]
```

 

**提示：**

- 树中结点数在范围 `[0, 104]` 内
- `-1000 <= Node.val <= 1000`

#### [1192. 查找集群内的「关键连接」](https://leetcode-cn.com/problems/critical-connections-in-a-network/)

难度困难185

力扣数据中心有 `n` 台服务器，分别按从 `0` 到 `n-1` 的方式进行了编号。它们之间以「服务器到服务器」点对点的形式相互连接组成了一个内部集群，其中连接 `connections` 是无向的。从形式上讲，`connections[i] = [a, b]` 表示服务器 `a` 和 `b` 之间形成连接。任何服务器都可以直接或者间接地通过网络到达任何其他服务器。

*「关键连接」* 是在该集群中的重要连接，也就是说，假如我们将它移除，便会导致某些服务器无法访问其他服务器。

请你以任意顺序返回该集群内的所有 「关键连接」。

 

**示例 1：**

**![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/critical-connections-in-a-network.png)**

```
输入：n = 4, connections = [[0,1],[1,2],[2,0],[1,3]]
输出：[[1,3]]
解释：[[3,1]] 也是正确的。
```

**示例 2:**

```
输入：n = 2, connections = [[0,1]]
输出：[[0,1]]
```

 

**提示：**

- `1 <= n <= 10^5`
- `n-1 <= connections.length <= 10^5`
- `connections[i][0] != connections[i][1]`
- 不存在重复的连接

#### [399. 除法求值](https://leetcode-cn.com/problems/evaluate-division/)

难度中等724

给你一个变量对数组 `equations` 和一个实数值数组 `values` 作为已知条件，其中 `equations[i] = [Ai, Bi]` 和 `values[i]` 共同表示等式 `Ai / Bi = values[i]` 。每个 `Ai` 或 `Bi` 是一个表示单个变量的字符串。

另有一些以数组 `queries` 表示的问题，其中 `queries[j] = [Cj, Dj]` 表示第 `j` 个问题，请你根据已知条件找出 `Cj / Dj = ?` 的结果作为答案。

返回 **所有问题的答案** 。如果存在某个无法确定的答案，则用 `-1.0` 替代这个答案。如果问题中出现了给定的已知条件中没有出现的字符串，也需要用 `-1.0` 替代这个答案。

**注意：**输入总是有效的。你可以假设除法运算中不会出现除数为 0 的情况，且不存在任何矛盾的结果。

 

**示例 1：**

```
输入：equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
输出：[6.00000,0.50000,-1.00000,1.00000,-1.00000]
解释：
条件：a / b = 2.0, b / c = 3.0
问题：a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ?
结果：[6.0, 0.5, -1.0, 1.0, -1.0 ]
```

**示例 2：**

```
输入：equations = [["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = [["a","c"],["c","b"],["bc","cd"],["cd","bc"]]
输出：[3.75000,0.40000,5.00000,0.20000]
```

**示例 3：**

```
输入：equations = [["a","b"]], values = [0.5], queries = [["a","b"],["b","a"],["a","c"],["x","y"]]
输出：[0.50000,2.00000,-1.00000,-1.00000]
```

 

**提示：**

- `1 <= equations.length <= 20`
- `equations[i].length == 2`
- `1 <= Ai.length, Bi.length <= 5`
- `values.length == equations.length`
- `0.0 < values[i] <= 20.0`
- `1 <= queries.length <= 20`
- `queries[i].length == 2`
- `1 <= Cj.length, Dj.length <= 5`
- `Ai, Bi, Cj, Dj` 由小写英文字母与数字组成

#### [572. 另一棵树的子树](https://leetcode-cn.com/problems/subtree-of-another-tree/)

难度简单694

给你两棵二叉树 `root` 和 `subRoot` 。检验 `root` 中是否包含和 `subRoot` 具有相同结构和节点值的子树。如果存在，返回 `true` ；否则，返回 `false` 。

二叉树 `tree` 的一棵子树包括 `tree` 的某个节点和这个节点的所有后代节点。`tree` 也可以看做它自身的一棵子树。

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/subtree1-tree.jpg)

```
输入：root = [3,4,5,1,2], subRoot = [4,1,2]
输出：true
```

**示例 2：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/subtree2-tree.jpg)

```
输入：root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
输出：false
```

 

**提示：**

- `root` 树上的节点数量范围是 `[1, 2000]`
- `subRoot` 树上的节点数量范围是 `[1, 1000]`
- `-104 <= root.val <= 104`
- `-104 <= subRoot.val <= 104`

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

#### [207. 课程表](https://leetcode-cn.com/problems/course-schedule/)

难度中等1217

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

 

**提示：**

- `1 <= numCourses <= 105`
- `0 <= prerequisites.length <= 5000`
- `prerequisites[i].length == 2`
- `0 <= ai, bi < numCourses`
- `prerequisites[i]` 中的所有课程对 **互不相同**

#### [994. 腐烂的橘子](https://leetcode-cn.com/problems/rotting-oranges/)

难度中等535

在给定的 `m x n` 网格 `grid` 中，每个单元格可以有以下三个值之一：

- 值 `0` 代表空单元格；
- 值 `1` 代表新鲜橘子；
- 值 `2` 代表腐烂的橘子。

每分钟，腐烂的橘子 **周围 4 个方向上相邻** 的新鲜橘子都会腐烂。

返回 *直到单元格中没有新鲜橘子为止所必须经过的最小分钟数。如果不可能，返回 `-1`* 。

 

**示例 1：**

**![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/02/16/oranges.png)**

```
输入：grid = [[2,1,1],[1,1,0],[0,1,1]]
输出：4
```

**示例 2：**

```
输入：grid = [[2,1,1],[0,1,1],[1,0,1]]
输出：-1
解释：左下角的橘子（第 2 行， 第 0 列）永远不会腐烂，因为腐烂只会发生在 4 个正向上。
```

**示例 3：**

```
输入：grid = [[0,2]]
输出：0
解释：因为 0 分钟时已经没有新鲜橘子了，所以答案就是 0 。
```

 

**提示：**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 10`
- `grid[i][j]` 仅为 `0`、`1` 或 `2`

#### [127. 单词接龙](https://leetcode-cn.com/problems/word-ladder/)

难度困难1002

字典 `wordList` 中从单词 `beginWord` 和 `endWord` 的 **转换序列** 是一个按下述规格形成的序列 `beginWord -> s1 -> s2 -> ... -> sk`：

- 每一对相邻的单词只差一个字母。
-  对于 `1 <= i <= k` 时，每个 `si` 都在 `wordList` 中。注意， `beginWord` 不需要在 `wordList` 中。
- `sk == endWord`

给你两个单词 `beginWord` 和 `endWord` 和一个字典 `wordList` ，返回 *从 `beginWord` 到 `endWord` 的 **最短转换序列** 中的 **单词数目*** 。如果不存在这样的转换序列，返回 `0` 。

**示例 1：**

```
输入：beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
输出：5
解释：一个最短转换序列是 "hit" -> "hot" -> "dot" -> "dog" -> "cog", 返回它的长度 5。
```

**示例 2：**

```
输入：beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
输出：0
解释：endWord "cog" 不在字典中，所以无法进行转换。
```

 

**提示：**

- `1 <= beginWord.length <= 10`
- `endWord.length == beginWord.length`
- `1 <= wordList.length <= 5000`
- `wordList[i].length == beginWord.length`
- `beginWord`、`endWord` 和 `wordList[i]` 由小写英文字母组成
- `beginWord != endWord`
- `wordList` 中的所有字符串 **互不相同**



#### [1293. 网格中的最短路径](https://leetcode-cn.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/)

难度困难174

给你一个 `m * n` 的网格，其中每个单元格不是 `0`（空）就是 `1`（障碍物）。每一步，您都可以在空白单元格中上、下、左、右移动。

如果您 **最多** 可以消除 `k` 个障碍物，请找出从左上角 `(0, 0)` 到右下角 `(m-1, n-1)` 的最短路径，并返回通过该路径所需的步数。如果找不到这样的路径，则返回 `-1` 。

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/short1-grid.jpg)

```
输入： grid = [[0,0,0],[1,1,0],[0,0,0],[0,1,1],[0,0,0]], k = 1
输出：6
解释：
不消除任何障碍的最短路径是 10。
消除位置 (3,2) 处的障碍后，最短路径是 6 。该路径是 (0,0) -> (0,1) -> (0,2) -> (1,2) -> (2,2) -> (3,2) -> (4,2).
```

**示例 2：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/short2-grid.jpg)

```
输入：grid = [[0,1,1],[1,1,1],[1,0,0]], k = 1
输出：-1
解释：我们至少需要消除两个障碍才能找到这样的路径。
```

#### [417. 太平洋大西洋水流问题](https://leetcode-cn.com/problems/pacific-atlantic-water-flow/)

难度中等362

有一个 `m × n` 的矩形岛屿，与 **太平洋** 和 **大西洋** 相邻。 **“太平洋”** 处于大陆的左边界和上边界，而 **“大西洋”** 处于大陆的右边界和下边界。

这个岛被分割成一个由若干方形单元格组成的网格。给定一个 `m x n` 的整数矩阵 `heights` ， `heights[r][c]` 表示坐标 `(r, c)` 上单元格 **高于海平面的高度** 。

岛上雨水较多，如果相邻单元格的高度 **小于或等于** 当前单元格的高度，雨水可以直接向北、南、东、西流向相邻单元格。水可以从海洋附近的任何单元格流入海洋。

返回 *网格坐标 `result` 的 **2D列表** ，其中 `result[i] = [ri, ci]` 表示雨水可以从单元格 `(ri, ci)` 流向 **太平洋和大西洋*** 。

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/waterflow-grid.jpg)

```
输入: heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]
输出: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
```

**示例 2：**

```
输入: heights = [[2,1],[1,2]]
输出: [[0,0],[0,1],[1,0],[1,1]]
```

 

**提示：**

- `m == heights.length`
- `n == heights[r].length`
- `1 <= m, n <= 200`
- `0 <= heights[r][c] <= 105`



