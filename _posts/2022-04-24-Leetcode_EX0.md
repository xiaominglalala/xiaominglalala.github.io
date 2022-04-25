---
layout:     post
title:      Exercise 0
subtitle:   
date:       2022-04-24
author:     Ethan
header-img: img/1.jpg
catalog: true
tags:
    - Leetcode
---

### 4/21-4/22 Meta 高频题

#### [1249. Minimum Remove to Make Valid Parentheses](https://leetcode-cn.com/problems/minimum-remove-to-make-valid-parentheses/)

难度中等178

Given a string s of `'('` , `')'` and lowercase English characters.

Your task is to remove the minimum number of parentheses ( `'('` or `')'`, in any positions ) so that the resulting *parentheses string* is valid and return **any** valid string.

Formally, a *parentheses string* is valid if and only if:

- It is the empty string, contains only lowercase characters, or
- It can be written as `AB` (`A` concatenated with `B`), where `A` and `B` are valid strings, or
- It can be written as `(A)`, where `A` is a valid string.

 

**Example 1:**

```
Input: s = "lee(t(c)o)de)"
Output: "lee(t(c)o)de"
Explanation: "lee(t(co)de)" , "lee(t(c)ode)" would also be accepted.
```

**Example 2:**

```
Input: s = "a)b(c)d"
Output: "ab(c)d"
```

**Example 3:**

```
Input: s = "))(("
Output: ""
Explanation: An empty string is also valid.
```

 

**Constraints:**

- `1 <= s.length <= 105`
- `s[i]` is either`'('` , `')'`, or lowercase English letter`.`

通过次数31,175

提交次数53,266

思路：

- *当且仅当* 满足以下条件时，字符串中的括号是平衡的：

  1. 字符串中有相同数量的 `"("` 和 `")"`。
  2. ![image-20220421142925596](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421142925596.png)

- 例如，`"L(ee)(t(()co)d)e"` 是一个 *平衡* 的字符串。下图展示该字符串的余量变化情况。

  ![该图显示字符串 L(ee)(t(()co)d)e 是平衡的](https://pic.leetcode-cn.com/Figures/1249/balance_example_1.png)

  ![image-20220421142949346](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421142949346.png)

- 如果最终结果大于0或者中间途中就出现小于0，都是有问题的

- 该问题要求删除最少括号，使得字符串有效。如何实现该目标？

- 使用 栈，每次遇到 "("，都将它的索引压入栈中。每次遇到 ")"，都从栈中移除一个索引，用该 ")" 与栈顶的 "(" 匹配。栈的深度等于余量。需要执行以下操作：

  - 如果在栈为空时遇到 ")"，则删除该 ")"，防止余量为负。
  - 如果扫描到字符串结尾有 "("，则删除它，防止余量不为 0

- ![image-20220421143758082](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220421143758082.png)

- 一开始放入1，然后遇到3，就pop

- 4和5满足栈为空但是是 ")"，必须删除

- 尽管可以在 O(n)的时间内完成删除操作，但是必须小心，因为一些意外情况会导致 O(n^2），因为一些 O(n)的操作有时也会被误认为是 O(1）。如果在面试中出现这些错误非常不好。

- 在 字符串 的 任意一个位置 添加、删除或更改一个字符的操作都是 O(n)O(n) 的，因为 String 是 不可变的。每次修改整个字符串都会重建。

  从 list，vector，array 的非最后一个位置添加或删除元素也是 O(n)O(n) 的，因为在其他索引操作需要创建新的空间或者填充空间。

  检查一个元素是否在 list 中，常使用 线性查找，即使二分查找也要 O(\log n)O(logn) 的复杂度，这并不是理想的效率。

- ![image-20220422002531341](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220422002531341.png)
- 一种安全策略是遍历字符串，然后将要保留的字符插入到 **list**（Python）。遍历完所有字符后，只需要一步 O*(*n) 的操作将其转换为字符串。
- 检查某个元素是否在 **集合** 中需要 O(1)
- `"".join(...)` 的复杂度都是 O(n)

代码：

![image-20220422004034461](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220422004034461.png)

  

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

![img](https://assets.leetcode.com/uploads/2021/01/28/vtree2.jpg)

```
Input: root = [3,9,8,4,0,1,7,null,null,null,2,5]
Output: [[4],[9,5],[3,0,1],[8,2],[7]]
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

思路：

- 通过题目描述，最直观的方法是BFS，我们希望维护一个哈希表，key would be the column, and value would be a list which contains the values of nodes in the same column
-  For BFS, we often use a  queue to keep track of the order to visit the nodes.
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
- During the BFS, we can know the range of column indeices
- At the end of BFS traversal, we would walk though [min_column, max_column] and find the results
- Time and space complexity should be O(n)

代码：

- 注意要对特殊情况，空输入进行判断，否则会报错，面试一定要注意
- ![image-20220422105250362](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220422105250362.png)
- ![image-20220422105331339](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220422105331339.png)



#### [680. Valid Palindrome II](https://leetcode-cn.com/problems/valid-palindrome-ii/)

难度简单487

Given a string `s`, return `true` *if the* `s` *can be palindrome after deleting **at most one** character from it*.

 

**Example 1:**

```
Input: s = "aba"
Output: true
```

**Example 2:**

```
Input: s = "abca"
Output: true
Explanation: You could delete the character 'c'.
```

**Example 3:**

```
Input: s = "abc"
Output: false
```

 

**Constraints:**

- `1 <= s.length <= 105`
- `s` consists of lowercase English letters.

思路：

- 回文数常见的思路就是双指针
- 用我原来的，"cupuuuupucu"有可能会不知道删头还是尾，不能 elif，都要试

![image-20220422114010588](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220422114010588.png)

#### [125. Valid Palindrome](https://leetcode-cn.com/problems/valid-palindrome/)

难度简单517

A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` *if it is a **palindrome**, or* `false` *otherwise*.

 

**Example 1:**

```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

**Example 2:**

```
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

**Example 3:**

```
Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
```

 

**Constraints:**

- `1 <= s.length <= 2 * 105`
- `s` consists only of printable ASCII characters.

思路：

- 使用.isalnum()来判断是不是字母或者数字
- 使用.lower()来获取小字母

代码：

![image-20220422122753127](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220422122753127.png)

时间空间复杂度都是O(n)

如果直接修改原来的s，空间将会变成O(1), 主要就是遇到空格就一直走到没空格，但注意这样的判断也要对front end判断

![image-20220422123232530](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220422123232530.png)

#### [234. Palindrome Linked List](https://leetcode-cn.com/problems/palindrome-linked-list/)

难度简单1358

Given the `head` of a singly linked list, return `true` if it is a palindrome.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

```
Input: head = [1,2,2,1]
Output: true
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/pal2linked-list.jpg)

```
Input: head = [1,2]
Output: false
```

 

**Constraints:**

- The number of nodes in the list is in the range `[1, 105]`.
- `0 <= Node.val <= 9`

 

**Follow up:** Could you do it in `O(n)` time and `O(1)` space?

思路：

- 把链表的值复制到list中，再赢125中的方法判断是否回文，时间空间复杂度都是O(N)
- 复制链表的值到list是O(n),双指针判断回文是O(n),
- 避免使用 O(n)额外空间的方法就是改变输入。我们可以将链表的后半部分反转（修改链表结构）,然后将前半部分和后半部分进行比较。使用快慢指针，快到尾，慢的刚好是中间
- 在并发环境下，函数运行时需要锁定其他线程或进程对链表的访问，因为在函数执行过程中链表会被修改。

- O(1)的第二次复习时在尝试把

代码：

![image-20220422130026091](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220422130026091.png)

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

#### 160. Intersection of Two Linked Lists

Easy

8606861Add to ListShare

Given the heads of two singly linked-lists `headA` and `headB`, return *the node at which the two lists intersect*. If the two linked lists have no intersection at all, return `null`.

For example, the following two linked lists begin to intersect at node `c1`:

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/160_statement.png)

The test cases are generated such that there are no cycles anywhere in the entire linked structure.

**Note** that the linked lists must **retain their original structure** after the function returns.

**Custom Judge:**

The inputs to the **judge** are given as follows (your program is **not** given these inputs):

- `intersectVal` - The value of the node where the intersection occurs. This is `0` if there is no intersected node.
- `listA` - The first linked list.
- `listB` - The second linked list.
- `skipA` - The number of nodes to skip ahead in `listA` (starting from the head) to get to the intersected node.
- `skipB` - The number of nodes to skip ahead in `listB` (starting from the head) to get to the intersected node.

The judge will then create the linked structure based on these inputs and pass the two heads, `headA` and `headB` to your program. If you correctly return the intersected node, then your solution will be **accepted**.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/05/160_example_1_1.png)

```
Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3
Output: Intersected at '8'
Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect).
From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,6,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/03/05/160_example_2.png)

```
Input: intersectVal = 2, listA = [1,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
Output: Intersected at '2'
Explanation: The intersected node's value is 2 (note that this must not be 0 if the two lists intersect).
From the head of A, it reads as [1,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
```

**Example 3:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/160_example_3.png)

```
Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
Output: No intersection
Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
```

 

**Constraints:**

- The number of nodes of `listA` is in the `m`.
- The number of nodes of `listB` is in the `n`.
- `1 <= m, n <= 3 * 104`
- `1 <= Node.val <= 105`
- `0 <= skipA < m`
- `0 <= skipB < n`
- `intersectVal` is `0` if `listA` and `listB` do not intersect.
- `intersectVal == listA[skipA] == listB[skipB]` if `listA` and `listB` intersect.

 

**Follow up:** Could you write a solution that runs in `O(m + n)` time and use only `O(1)` memory?

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220423210137531.png" alt="image-20220423210137531" style="zoom: 67%;" />

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

#### [1570. Dot Product of Two Sparse Vectors](https://leetcode-cn.com/problems/dot-product-of-two-sparse-vectors/)

难度中等20

Given two sparse vectors, compute their dot product.

Implement class `SparseVector`:

- `SparseVector(nums)` Initializes the object with the vector `nums`
- `dotProduct(vec)` Compute the dot product between the instance of *SparseVector* and `vec`

A **sparse vector** is a vector that has mostly zero values, you should store the sparse vector **efficiently** and compute the dot product between two *SparseVector*.

**Follow up:** What if only one of the vectors is sparse?

 

**Example 1:**

```
Input: nums1 = [1,0,0,2,3], nums2 = [0,3,0,4,0]
Output: 8
Explanation: v1 = SparseVector(nums1) , v2 = SparseVector(nums2)
v1.dotProduct(v2) = 1*0 + 0*3 + 0*0 + 2*4 + 3*0 = 8
```

**Example 2:**

```
Input: nums1 = [0,1,0,0,0], nums2 = [0,0,0,0,2]
Output: 0
Explanation: v1 = SparseVector(nums1) , v2 = SparseVector(nums2)
v1.dotProduct(v2) = 0*0 + 1*0 + 0*0 + 0*0 + 0*2 = 0
```

**Example 3:**

```
Input: nums1 = [0,1,0,0,2,0,0], nums2 = [1,0,0,0,3,0,4]
Output: 6
```

 

**Constraints:**

- `n == nums1.length == nums2.length`
- `1 <= n <= 10^5`
- `0 <= nums1[i], nums2[i] <= 100`

思路：

- 如果是不考虑稀疏情况，只需要单纯的遍历求和
- ![image-20220423172811423](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220423172811423.png)
- 对于稀疏情况，需要记录不为0的部分
- 注意使用.items()来获取值
- 注意是list1.dotProduct(list2)，说明self给list1，list2用，dotProduct给list2用

代码：

![image-20220423174105640](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220423174105640.png)

- Time complexity: O(n) for creating the Hash Map; O(L) for calculating the dot product.
- Space complexity: O(L) for creating the Hash Map, as we only store elements that are non-zero. O(1) for calculating the dot product.

#### [408. Valid Word Abbreviation](https://leetcode-cn.com/problems/valid-word-abbreviation/)

难度简单39

A string can be **abbreviated** by replacing any number of **non-adjacent**, **non-empty** substrings with their lengths. The lengths **should not** have leading zeros.

For example, a string such as `"substitution"` could be abbreviated as (but not limited to):

- `"s10n"` (`"s ubstitutio n"`)
- `"sub4u4"` (`"sub stit u tion"`)
- `"12"` (`"substitution"`)
- `"su3i1u2on"` (`"su bst i t u ti on"`)
- `"substitution"` (no substrings replaced)

The following are **not valid** abbreviations:

- `"s55n"` (`"s ubsti tutio n"`, the replaced substrings are adjacent)
- `"s010n"` (has leading zeros)
- `"s0ubstitution"` (replaces an empty substring)

Given a string `word` and an abbreviation `abbr`, return *whether the string **matches** the given abbreviation*.

A **substring** is a contiguous **non-empty** sequence of characters within a string.

 

**Example 1:**

```
Input: word = "internationalization", abbr = "i12iz4n"
Output: true
Explanation: The word "internationalization" can be abbreviated as "i12iz4n" ("i nternational iz atio n").
```

**Example 2:**

```
Input: word = "apple", abbr = "a2e"
Output: false
Explanation: The word "apple" cannot be abbreviated as "a2e".
```

 

**Constraints:**

- `1 <= word.length <= 20`
- `word` consists of only lowercase English letters.
- `1 <= abbr.length <= 10`
- `abbr` consists of lowercase English letters and digits.
- All the integers in `abbr` will fit in a 32-bit integer.

思路：

- 使用双指针的方法，一个给word，一个给abbr
- 如果abbr的指针碰到了数字，先判断是不是0，是0直接false；不是0，不停动abbr的指针，直到不是数字，然后求出这个数值，然后将word的指针加上这个值
- 如果abbr碰到的不是指针，就要判断两个字符是不是相等
- while的终止条件是两个指针有一个走到头，最后出去要判断两个指针是不是都到头了。

代码：

![image-20220423171856016](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220423171856016.png)

