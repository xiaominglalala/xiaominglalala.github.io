---
layout:     post
title:      Binary Tree Exercise 2
subtitle:   
date:       2022-05-08
author:     Ethan
header-img: img/10.jpg
catalog: true
tags:
    - Leetcode
    - Binary Tree

---

## Binary Tree Exercise 2

#### 1.1 深度优先遍历使用的数据结构（栈）：

在深度优先遍历的过程中，需要将 当前遍历到的结点 的相邻结点 暂时保存 起来，以便在回退的时候可以继续访问它们。遍历到的结点的顺序呈现「后进先出」的特点，因此 深度优先遍历可以通过「栈」实现。

在Python中，列表就满足后进先出的要求（append，pop）

对于之前做过的二叉树的前中后序遍历，使用recursion（递归）是很容易想到的，但是使用iteration是比较难的，也是可能会被作为follow up的考点。推荐DFS都使用recursion来实现

![image-20220417084221574](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417084221574.png)

主要是掌握前中后序的迭代和递归写法

#### 1.2 广度优先遍历使用的数据结构（队列）：

#### 1.3 树的深度优先搜索：

- 「根结点 → 右子树 → 左子树」
- ![image-20220416234821547](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220416234821547.png)
- 前序（preorder）遍历：<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220416235111780.png" alt="image-20220416235111780" style="zoom: 67%;" />
- 中序(Inorder)遍历
- <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220416235225435.png" alt="image-20220416235225435" style="zoom:67%;" />
- 后序(Posorder)遍历
- <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417085922348.png" alt="image-20220417085922348" style="zoom:67%;" />

> 后序遍历最为重要

Preorder Binary Tree (Iteration)

- 前序遍历是中左右；
- <img src="https://pic.leetcode-cn.com/6233a9685447d0b4d7b513f739151ca065e5697e24070bcafc1ee5d28f9155a6.png" alt="中序遍历流程图" style="zoom: 33%;" />
- ![image-20220417100825910](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417100825910.png)

Preorder Binary Tree (Recursion)

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220217135851527.png" alt="image-20220217135851527" style="zoom: 67%;" />

Postorder Binary Tree (Iteration)

- 对于后序遍历的迭代法，就基本改一下前序遍历中的内容即可
- 前序遍历是中左右，后序遍历是左右中
- 那么我们只需要压入左右时和前序换一下，先压入左再压入右
- 最后反转数组

![image-20220417102432062](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417102432062.png)

注意不可以return list.reverse()

![image-20220417102509035](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417102509035.png)

Postorder Binary Tree (Recursion)

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417102542959.png" alt="image-20220417102542959" style="zoom:50%;" />

Inorder Binary Tree (Iteration)

- 前序遍历的顺序是中左右, 而对于一个binary tree, 先访问的元素是中间节点，要处理的元素也是中间节点。**前序要访问的元素和要处理的元素顺序是一致的，都是中间节点。**
- 中序遍历的顺序是左中右，先访问的是二叉树顶部的节点，然后一层一层向下访问，直到到达树左面的最底部，再开始处理节点（也就是在把节点的数值放进result数组中）就造成了**处理顺序和访问顺序是不一致的。**
- **使用迭代法写中序遍历，就需要借用指针的遍历来帮助访问节点，栈则用来处理节点上的元素。**

![image-20220417103649282](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417103649282.png)



Inorder Binary Tree (Recursion)

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220217142708700.png" alt="image-20220217142708700" style="zoom: 67%;" />

> 之后再考虑下N叉树的iteration

### 

#### [235. Lowest Common Ancestor of a Binary Search Tree](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

难度简单822

Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/binarysearchtree_improved.png)

```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/binarysearchtree_improved.png)

```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
Output: 2
Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.
```

**Example 3:**

```
Input: root = [2,1], p = 2, q = 1
Output: 2
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[2, 105]`.
- `-109 <= Node.val <= 109`
- All `Node.val` are **unique**.
- `p != q`
- `p` and `q` will exist in the BST.

思路：

注意二叉搜索树的特点是左边比中间小，右边比中间大

二叉树不是这样的，两边是什么都可以

如果采用递归的方法：

- 从根节点开始遍历树。
- 如果两个节点`p`和`q`都在右子树中，则从步骤 1 开始以右子树继续搜索。
- 如果两个节点`p`都`q`在左子树中，则从第 1 步开始从左子树继续搜索。
- 如果第 2 步和第 3 步都不为真，这意味着我们找到了 node`p`和`q`的子树共有的节点。因此我们将这个公共节点作为 LCA 返回。
- Time Complexity: O(N)*O*(*N*), where N*N* is the number of nodes in the BST. In the worst case we might be visiting all the nodes of the BST.
- Space Complexity: O(N)*O*(*N*). This is because the maximum amount of space utilized by the recursion stack would be N*N* since the height of a skewed BST could be N*N*.

代码：

![image-20220423191043294](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220423191043294.png)

- 注意递归要return和self

#### [236. Lowest Common Ancestor of a Binary Tree](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

难度中等1704

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```

**Example 3:**

```
Input: root = [1,2], p = 1, q = 2
Output: 1
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[2, 105]`.
- `-109 <= Node.val <= 109`
- All `Node.val` are **unique**.
- `p != q`
- `p` and `q` will exist in the tree.

思路

- 这题不再是二叉搜索树，而是二叉树
- ![image-20220423193628859](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220423193628859.png)
- `dfs`从根向下到它的子节点，如果是t`root == p`或`root == q`then root`必须是它们的LCA。
- 如果`left`子树包含后代（`p`或`q`）之一，而`right`子树包含剩余的后代（`q`或`p`），则`root`是它们的 LCA。
- 如果`left`子树同时包含两者`p`，`q`则`left`作为它们的 LCA 返回。
- 如果`right`子树同时包含两者`p`，`q`则`right`作为它们的 LCA 返回。

代码

![image-20220425000625972](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220425000625972.png)

#### [314. Binary Tree Vertical Order Traversal](https://leetcode-cn.com/problems/binary-tree-vertical-order-traversal/)

难度中等165

Given the `root` of a binary tree, return ***the vertical order traversal** of its nodes' values*. (i.e., from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from **left to right**.

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/vtree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[9],[3,15],[20],[7]]
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/vtree2-1.jpg)

```
Input: root = [3,9,8,4,0,1,7]
Output: [[4],[9],[3,0,1],[8],[7]]
```

**Example 3:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/vtree2.jpg)

```
Input: root = [3,9,8,4,0,1,7,null,null,null,2,5]
Output: [[4],[9,5],[3,0,1],[8,2],[7]]
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

思路：

- 通过题目描述，最直观的方法是BFS，我们希望维护一个哈希表，key would be the column, and value would be a list which contains the values of nodes in the same column
- For BFS, we often use a  queue to keep track of the order to visit the nodes.
- At each iteration within the BFS, we pop out an element from the queue. And it should tell us column index and node value 
- Then we put its children nodes into column - 1 and column + 1
- In the end, we sort the hash table by its key: column index
- ![image-20220422103305910](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220422103305910.png)

Complexity Analysis

- Time Complexity: O(nlgn)
  For BFS traversal, we traversed each node once and only once, O(n)
  We sorted the hash table by its keys. It should be O(nlgn), if the binary tree is extremely imbalanced, it would be O(nlgn)
- Space Complexity: O(n)
  Hash Table: O(n)
  During the BFS traversal, we use a queue to keep track of the next node to visit. For binary tree, the max number of nodes would be (N+1)/2, which is also the number of leafs in a full binary tree. SO it should be O(n)

代码：

![image-20220422103939548](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220422103939548.png)

Improve:

思路：

-  we can simply ***iterate***  to generate the outputs without need for sorting
-  During the BFS, we can know the range of column indeices
-  At the end of BFS traversal, we would walk though [min_column, max_column] and find the results
-  Time and space complexity should be O(n)

代码：

- 注意要对特殊情况，空输入进行判断，否则会报错，面试一定要注意
- ![image-20220422105250362](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220422105250362.png)
- ![image-20220422105331339](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220422105331339.png)



#### [1644. Lowest Common Ancestor of a Binary Tree II](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree-ii/)

难度中等24

Given the `root` of a binary tree, return *the lowest common ancestor (LCA) of two given nodes,* `p` *and* `q`. If either node `p` or `q` **does not exist** in the tree, return `null`. All values of the nodes in the tree are **unique**.

According to the **[definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor)**: "The lowest common ancestor of two nodes `p` and `q` in a binary tree `T` is the lowest node that has both `p` and `q` as **descendants** (where we allow **a node to be a descendant of itself**)". A **descendant** of a node `x` is a node `y` that is on the path from node `x` to some leaf node.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5. A node can be a descendant of itself according to the definition of LCA.
```

**Example 3:**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 10
Output: null
Explanation: Node 10 does not exist in the tree, so return null.
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `-109 <= Node.val <= 109`
- All `Node.val` are **unique**.
- `p != q`

 

**Follow up:** Can you find the LCA traversing the tree, without checking nodes existence?

思路：

- 这道题和上一题的区别在于p和q不一定存在于tree中，相比起上一题需要记录是否找到p和q
- 注意这里面对于root和p，q的判断应该发生在对 children 的递归调用之后。因为我们需要遍历所有节点。
- 这是和236不同的地方

代码：

![image-20220424235144556](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220424235144556.png)

#### [1650. Lowest Common Ancestor of a Binary Tree III](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree-iii/)

难度中等27

Given two nodes of a binary tree `p` and `q`, return *their lowest common ancestor (LCA)*.

Each node will have a reference to its parent node. The definition for `Node` is below:

```
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node parent;
}
```

According to the **[definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor)**: "The lowest common ancestor of two nodes p and q in a tree T is the lowest node that has both p and q as descendants (where we allow **a node to be a descendant of itself**)."

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5 since a node can be a descendant of itself according to the LCA definition.
```

**Example 3:**

```
Input: root = [1,2], p = 1, q = 2
Output: 1
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[2, 105]`.
- `-109 <= Node.val <= 109`
- All `Node.val` are **unique**.
- `p != q`
- `p` and `q` exist in the tree.

思路：

- 因为可以找parent，所以可以p和q同时网上面找
- 如果使用哈希表面试会失败。应该在 O(1) 空间中求解。用哈希表（查找时间复杂度为O(1)）记录已经走过的结点，重合的结点即为答案
- 此题去除其他节点，只看从给定的两个节点到根节点路径上的所有节点，则其可等效为双链表的交点问题
- 设两个指针分别从两个给定节点出发，如果两个节点不等，则继续往前一步。如果某个节点到达根节点，则跳到另一个给定的节点。最终两个指针一定会相遇在交点处,因为到交点处的路径上面指针走过的路程为L1 + L3 + L2,下面的指针走过的路程为L2 + L3 + L1
- 这道题和160题链表相交的思路一样

代码：

![image-20220423202129581](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220423202129581.png)

判断的时候删掉parent也可以，不知道为什么160不行

![image-20220423210304405](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220423210304405.png)

#### [2096. Step-By-Step Directions From a Binary Tree Node to Another](https://leetcode-cn.com/problems/step-by-step-directions-from-a-binary-tree-node-to-another/)

难度中等34

You are given the `root` of a **binary tree** with `n` nodes. Each node is uniquely assigned a value from `1` to `n`. You are also given an integer `startValue` representing the value of the start node `s`, and a different integer `destValue` representing the value of the destination node `t`.

Find the **shortest path** starting from node `s` and ending at node `t`. Generate step-by-step directions of such path as a string consisting of only the **uppercase** letters `'L'`, `'R'`, and `'U'`. Each letter indicates a specific direction:

- `'L'` means to go from a node to its **left child** node.
- `'R'` means to go from a node to its **right child** node.
- `'U'` means to go from a node to its **parent** node.

Return *the step-by-step directions of the **shortest path** from node* `s` *to node* `t`.

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/eg1.png)

```
Input: root = [5,1,2,3,null,6,4], startValue = 3, destValue = 6
Output: "UURL"
Explanation: The shortest path is: 3 → 1 → 5 → 2 → 6.
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/11/15/eg2.png)

```
Input: root = [2,1], startValue = 2, destValue = 1
Output: "L"
Explanation: The shortest path is: 2 → 1.
```

 

**Constraints:**

- The number of nodes in the tree is `n`.
- `2 <= n <= 105`
- `1 <= Node.val <= n`
- All the values in the tree are **unique**.
- `1 <= startValue, destValue <= n`
- `startValue != destValue`

#### [1740. 找到二叉树中的距离](https://leetcode-cn.com/problems/find-distance-in-a-binary-tree/)

难度中等14

给定一棵二叉树的根节点 `root` 以及两个整数 `p` 和 `q` ，返回该二叉树中值为 `p` 的结点与值为 `q` 的结点间的 **距离** 。

两个结点间的 **距离** 就是从一个结点到另一个结点的路径上边的数目。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
输入：root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 0
输出：3
解释：在 5 和 0 之间有 3 条边：5-3-1-0
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
输入：root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 7
输出：2
解释：在 5 和 7 之间有 2 条边：5-2-7
```

**示例 3：**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
输入：root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 5
输出：0
解释：一个结点与它本身之间的距离为 0
```

 

**提示：**

- 树中结点个数的范围在 `[1, 104]`.
- `0 <= Node.val <= 109`
- 树中所有结点的值都是唯一的.
- `p` 和`q` 是树中结点的值.

#### [938. 二叉搜索树的范围和](https://leetcode-cn.com/problems/range-sum-of-bst/)

难度简单286

给定二叉搜索树的根结点 `root`，返回值位于范围 *`[low, high]`* 之间的所有结点的值的和。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/05/bst1.jpg)

```
输入：root = [10,5,15,3,7,null,18], low = 7, high = 15
输出：32
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/11/05/bst2.jpg)

```
输入：root = [10,5,15,3,7,13,18,1,null,6], low = 6, high = 10
输出：23
```

 

**提示：**

- 树中节点数目在范围 `[1, 2 * 104]` 内
- `1 <= Node.val <= 105`
- `1 <= low <= high <= 105`
- 所有 `Node.val` **互不相同**

#### [987. 二叉树的垂序遍历](https://leetcode-cn.com/problems/vertical-order-traversal-of-a-binary-tree/)

难度困难189

给你二叉树的根结点 `root` ，请你设计算法计算二叉树的 **垂序遍历** 序列。

对位于 `(row, col)` 的每个结点而言，其左右子结点分别位于 `(row + 1, col - 1)` 和 `(row + 1, col + 1)` 。树的根结点位于 `(0, 0)` 。

二叉树的 **垂序遍历** 从最左边的列开始直到最右边的列结束，按列索引每一列上的所有结点，形成一个按出现位置从上到下排序的有序列表。如果同行同列上有多个结点，则按结点的值从小到大进行排序。

返回二叉树的 **垂序遍历** 序列。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/29/vtree1.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：[[9],[3,15],[20],[7]]
解释：
列 -1 ：只有结点 9 在此列中。
列  0 ：只有结点 3 和 15 在此列中，按从上到下顺序。
列  1 ：只有结点 20 在此列中。
列  2 ：只有结点 7 在此列中。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/01/29/vtree2.jpg)

```
输入：root = [1,2,3,4,5,6,7]
输出：[[4],[2],[1,5,6],[3],[7]]
解释：
列 -2 ：只有结点 4 在此列中。
列 -1 ：只有结点 2 在此列中。
列  0 ：结点 1 、5 和 6 都在此列中。
          1 在上面，所以它出现在前面。
          5 和 6 位置都是 (2, 0) ，所以按值从小到大排序，5 在 6 的前面。
列  1 ：只有结点 3 在此列中。
列  2 ：只有结点 7 在此列中。
```

**示例 3：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/vtree3.jpg)

```
输入：root = [1,2,3,4,6,5,7]
输出：[[4],[2],[1,5,6],[3],[7]]
解释：
这个示例实际上与示例 2 完全相同，只是结点 5 和 6 在树中的位置发生了交换。
因为 5 和 6 的位置仍然相同，所以答案保持不变，仍然按值从小到大排序。
```

 

**提示：**

- 树中结点数目总数在范围 `[1, 1000]` 内
- `0 <= Node.val <= 1000`