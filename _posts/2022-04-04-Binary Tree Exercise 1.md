layout:     post
title:      Binary Tree Exercise 1
subtitle:   
date:       2022-04-04
author:     Ethan
header-img: img/city_3.jpg
catalog: true
tags:
    - Leetcode
        - Binary Tree

##    Binary Tree Exercise 1

### 二叉树：

- 深度优先遍历
  - 前序遍历（递归法，迭代法）
  - 中序遍历（递归法，迭代法）
  - 后序遍历（递归法，迭代法）
- 广度优先遍历
  - 层次遍历（迭代法）

如何分别前中后序遍历？关键就是中间节点在哪里？

- ==前序遍历：**中**左右==
- ==中序遍历：左**中**右==
- ==后序遍历：左右**中**==

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220217134233435.png" alt="image-20220217134233435" style="zoom:50%;" />



### 二叉搜索树：

二叉搜索树是有数值的了，**二叉搜索树是一个有序树**。

- 若它的左子树不空，则左子树上所有结点的值均小于它的根结点的值；
- 若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值；
- 它的左、右子树也分别为二叉排序树

下面这两棵树都是搜索树 ![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20200806190304693.png)

### 平衡二叉搜索树

平衡二叉搜索树：又被称为AVL（Adelson-Velsky and Landis）树，且具有以下性质：它是一棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。

如图：

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/20200806190511967.png)

最后一棵 不是平衡二叉树，因为它的左右两个子树的高度差的绝对值超过了1。

### 1.二叉树的深度优先遍历（前中后序）（递归法）

> 迭代太蠢了，递归会简单，但是要回iteration的写法防止被考到
>

#### [144. 二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

难度简单728

给你二叉树的根节点 `root` ，返回它节点值的 **前序** 遍历。

 

**示例 1：**

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/inorder_1.jpg" alt="img" style="zoom:50%;" />

```
输入：root = [1,null,2,3]
输出：[1,2,3]
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

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/inorder_5.jpg" alt="img" style="zoom:50%;" />

```
输入：root = [1,2]
输出：[1,2]
```

**示例 5：**

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/inorder_4.jpg" alt="img" style="zoom:50%;" />

```
输入：root = [1,null,2]
输出：[1,2]
```

思路：

- 写递归法，需要三要素
  - 首先是确定这个递归函数的参数和返回类型：对于前序遍历，就是输入当前节点
  - 确认终止条件：如果当前节点为空，则return
  - 确认每次递归的内容：如果当前节点不为空，则输出当前节点，再递归left，再递归right
  - 前序是preorder

代码：

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220217134834347.png" alt="image-20220217134834347" style="zoom: 67%;" />

递归算法很简单，你可以通过迭代算法完成吗？

Preorder Binary Tree (Iteration)

- 前序遍历是中左右；
- <img src="https://pic.leetcode-cn.com/6233a9685447d0b4d7b513f739151ca065e5697e24070bcafc1ee5d28f9155a6.png" alt="中序遍历流程图" style="zoom: 33%;" />
- 注意要判断node.right,之前recursion不需要判断这个
- 而且这里要初始化node
- 先把中间pop，然后中间的val放入result，再把右放入stack，再把左放入stack；这样的pop出来是中左右
- ![image-20220417100825910](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417100825910.png)

- Time complexity : we visit each node exactly once, thus the time complexity isO(*N*), 
- Space complexity : depending on the tree structure, we could keep up to the entire tree, therefore, the space complexity is O(*N*).

![image-20220508193146490](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220508193146490.png)

#### [145. 二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

难度简单755

给你一棵二叉树的根节点 `root` ，返回其节点值的 **后序遍历** 。

 

**示例 1：**

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/pre1.jpg" alt="img" style="zoom:50%;" />

```
输入：root = [1,null,2,3]
输出：[3,2,1]
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

思路：

和上面的几乎一样，调整一下单次迭代内的执行顺序

代码：

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220217135851527.png" alt="image-20220217135851527" style="zoom: 67%;" />

Postorder Binary Tree (Iteration)

- 对于后序遍历的迭代法，就基本改一下前序遍历中的内容即可
- 前序遍历是中左右，后序遍历是左右中
- 那么我们只需要压入左右时和前序换一下，先压入左再压入右
- 最后反转数组
- 注意不可以先左右再中，这将会和中序遍历一样，由于访问元素的顺序和处理的顺序不同，一开始访问的中间已经不去处理，就会有问题

![image-20220417102432062](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417102432062.png)

注意不可以return list.reverse()

![image-20220417102509035](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417102509035.png)



![image-20220508193128400](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220508193128400.png)

#### [94. 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

难度简单1269

给定一个二叉树的根节点 `root` ，返回它的 **中序** 遍历。

 

**示例 1：**

<img src="https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg" alt="img" style="zoom:50%;" />

```
输入：root = [1,null,2,3]
输出：[1,3,2]
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

<img src="https://assets.leetcode.com/uploads/2020/09/15/inorder_5.jpg" alt="img" style="zoom:50%;" />

```
输入：root = [1,2]
输出：[2,1]
```

**示例 5：**

<img src="https://assets.leetcode.com/uploads/2020/09/15/inorder_4.jpg" alt="img" style="zoom:50%;" />

```
输入：root = [1,null,2]
输出：[1,2]
```

代码：

<img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220217142708700.png" alt="image-20220217142708700" style="zoom: 67%;" />

Inorder Binary Tree (Iteration)

- 前序遍历的顺序是中左右, 而对于一个binary tree, 先访问的元素是中间节点，要处理的元素也是中间节点。**前序要访问的元素和要处理的元素顺序是一致的，都是中间节点。**
- 中序遍历的顺序是左中右，先访问的是二叉树顶部的节点，然后一层一层向下访问，直到到达树左面的最底部，再开始处理节点（也就是在把节点的数值放进result数组中）就造成了**处理顺序和访问顺序是不一致的。**
- **使用迭代法写中序遍历，就需要借用指针的遍历来帮助访问节点，栈则用来处理节点上的元素。**
- 注意一开始不把root放进去，while是对node和stack都判断
- 对于node还没走到最左边，就一直走，走的路上每个左节点都压入stack
- 终于走到了最左边，再把节点的值放入result，然后让他变成右边的

![image-20220417103649282](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220417103649282.png)

- 上面那个不好，这个模板三个顺序就能统一了，区别主要在于要判断node是不是None, 是None就说明要处理
- 通过添加None来提醒我们这个节点要提出来处理

![image-20220508192333014](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220508192333014.png)

#### [589. N 叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/)

难度简单207

给定一个 n 叉树的根节点  `root` ，返回 *其节点值的 **前序遍历*** 。

n 叉树 在输入中按层序遍历进行序列化表示，每组子节点由空值 `null` 分隔（请参见示例）。


**示例 1：**

<img src="https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png" alt="img" style="zoom:67%;" />

```
输入：root = [1,null,3,2,4,null,5,6]
输出：[1,3,5,6,2,4]
```

**示例 2：**

<img src="https://assets.leetcode.com/uploads/2019/11/08/sample_4_964.png" alt="img" style="zoom:67%;" />

```
输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
输出：[1,2,3,6,7,11,14,4,8,12,5,9,13,10]
```

思路：

代码：

对于子节点，不存在左右了，就全部traversal

<img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220221121238273.png" alt="image-20220221121238273" style="zoom:67%;" />

对于迭代法，注意21行是extend

![image-20220509191013260](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220509191013260.png)

![image-20220509191145790](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220509191145790.png)

#### [590. N 叉树的后序遍历](https://leetcode-cn.com/problems/n-ary-tree-postorder-traversal/)

难度简单178

给定一个 n 叉树的根节点 `root` ，返回 *其节点值的 **后序遍历*** 。

n 叉树 在输入中按层序遍历进行序列化表示，每组子节点由空值 `null` 分隔（请参见示例）。

 

**示例 1：**

<img src="https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png" alt="img" style="zoom:67%;" />

```
输入：root = [1,null,3,2,4,null,5,6]
输出：[5,6,3,2,4,1]
```

**示例 2：**

<img src="https://assets.leetcode.com/uploads/2019/11/08/sample_4_964.png" alt="img" style="zoom:67%;" />

```
输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
输出：[2,6,14,11,7,3,12,8,4,13,9,10,5,1]
```

思路：

- 注意要内置一个函数，然后参数只需要root，不需要result

代码：

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220221120649991.png" alt="image-20220221120649991" style="zoom:67%;" />

### 2.二叉树的广度优先遍历（层序遍历）（迭代）

- 前面的是深度优先遍历，现在是二叉树另外一种遍历：层序遍历。层序遍历是一层一层的遍历：用**队列**来实现，**队列先进先出，符合一层一层遍历的逻辑**
- ![102二叉树的层序遍历](https://tva1.sinaimg.cn/large/008eGmZEly1gnad5itmk8g30iw0cqe83.gif)

#### [102. 二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

难度中等1179

给你二叉树的根节点 `root` ，返回其节点值的 **层序遍历** 。 （即逐层地，从左到右访问所有节点）。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：[[3],[9,20],[15,7]]
```

**示例 2：**

```
输入：root = [1]
输出：[[1]]
```

**示例 3：**

```
输入：root = []
输出：[]
```

思路：

- 和深度优先遍历一样，同样是有递归法和迭代法
- 不同于深度优先遍历使用递归，广度优先使用迭代会更好理解
- 借助python的内置队列deque，调用方法是：`from collections import deque`
- deque相比list的好处是，list的pop(0)是O(n)复杂度，deque的popleft()是O(1)复杂度；把输入的root转换为deque的方法：`que = deque([root])`
- 循环的终止条件是que的所有元素都popleft出去，按照需求放在了result里面
- 注意是每层都要一个[],所以再while外面，我们需要一个`result`，而在每次执行while时，要一个`sub_result`，最后append到`result`里面
- 注意给我们的二叉树根节点列表，这个列表看起来就是层次遍历，但是会有null，而且实际的是有left和right的，不是单纯的val的列表。是我们要输出的是单纯的val列表
- 对于每次val，把cur给popleft出来，放在sub_result里面。再吧cur的left和right给放在que后面，用于下一次的result；而下一次当看到之前提到的left和right，
  ![102二叉树的层序遍历](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/008eGmZEly1gnad5itmk8g30iw0cqe83.gif)

代码：

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220217174904929.png" alt="image-20220217174904929" style="zoom:67%;" />
注意23，25行放入的是TreeNode,而不是val

#### [107. 二叉树的层序遍历 II](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/)

难度中等535

给你二叉树的根节点 `root` ，返回其节点值 **自底向上的层序遍历** 。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/tree1.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：[[15,7],[9,20],[3]]
```

**示例 2：**

```
输入：root = [1]
输出：[[1]]
```

**示例 3：**

```
输入：root = []
输出：[]
```

思路：

- 相对于上一题的结果，只要反转一下list就可以了：`result.reverse()`或者result = reversed(result) 
- 注意不需要`result=result.reverse()`, 也不能`return result.reverse()`

代码：

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220217180333451.png" alt="image-20220217180333451" style="zoom:67%;" />

#### [199. 二叉树的右视图](https://leetcode-cn.com/problems/binary-tree-right-side-view/)

难度中等621

给定一个二叉树的 **根节点** `root`，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/02/14/tree.jpg)

```
输入: [1,2,3,null,5,null,4]
输出: [1,3,4]
```

**示例 2:**

```
输入: [1,null,3]
输出: [1,3]
```

**示例 3:**

```
输入: []
输出: []
```

思路：

提取每个sub_result的最后一个[-1]

代码：

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220217182147679.png" alt="image-20220217182147679" style="zoom:67%;" />

#### [637. 二叉树的层平均值](https://leetcode-cn.com/problems/average-of-levels-in-binary-tree/)

难度简单311

给定一个非空二叉树的根节点 `root` , 以数组的形式返回每一层节点的平均值。与实际答案相差 `10-5` 以内的答案可以被接受。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/03/09/avg1-tree.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：[3.00000,14.50000,11.00000]
解释：第 0 层的平均值为 3,第 1 层的平均值为 14.5,第 2 层的平均值为 11 。
因此返回 [3, 14.5, 11] 。
```

**示例 2:**

![img](https://assets.leetcode.com/uploads/2021/03/09/avg2-tree.jpg)

```
输入：root = [3,9,20,15,7]
输出：[3.00000,14.50000,11.00000]
```

思路：

- 每层求sum/len后，再加到result

代码：

<img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220218152151298.png" alt="image-20220218152151298" style="zoom:67%;" />

#### [429. N 叉树的层序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)

难度中等199

给定一个 N 叉树，返回其节点值的*层序遍历*。（即从左到右，逐层遍历）。

树的序列化输入是用层序遍历，每组子节点都由 null 值分隔（参见示例）。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png)

```
输入：root = [1,null,3,2,4,null,5,6]
输出：[[1],[3,2,4],[5,6]]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2019/11/08/sample_4_964.png)

```
输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
输出：[[1],[2,3,4,5],[6,7,8,9,10],[11,12,13],[14]]
```

思路：

- 由于每行不再是left和right，所以对于que不再是用`append`，而是用`extend`
- ![image-20220218153310541](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220218153310541.png)

代码：

<img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220218153501795.png" alt="image-20220218153501795" style="zoom:67%;" />

#### [515. 在每个树行中找最大值](https://leetcode-cn.com/problems/find-largest-value-in-each-tree-row/)

难度中等169

给定一棵二叉树的根节点 `root` ，请找出该二叉树中每一层的最大值。

 

**示例1：**

![img](https://assets.leetcode.com/uploads/2020/08/21/largest_e1.jpg)

```
输入: root = [1,3,2,5,3,null,9]
输出: [1,3,9]
```

**示例2：**

```
输入: root = [1,2,3]
输出: [1,3]
```

思路：

代码：

<img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220218154518167.png" alt="image-20220218154518167" style="zoom:67%;" />

#### [116. 填充每个节点的下一个右侧节点指针](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/)

难度中等676

给定一个 **完美二叉树** ，其所有叶子节点都在同一层，每个父节点都有两个子节点。二叉树定义如下：

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 `NULL`。

初始状态下，所有 next 指针都被设置为 `NULL`。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2019/02/14/116_sample.png)

```
输入：root = [1,2,3,4,5,6,7]
输出：[1,#,2,3,#,4,5,6,7,#]
解释：给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。序列化的输出按层序遍历排列，同一层节点由 next 指针连接，'#' 标志着每一层的结束。
```



**示例 2:**

```
输入：root = []
输出：[]
```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 212 - 1]`.
- `-1000 <= Node.val <= 1000`

 

**Follow-up:**

- You may only use constant extra space.
- The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.

思路：

别想复杂了，就是que弹出来的那个，让他的next为que[0]，也就是目前que中的第一个。当然也需要长度判断来看是不是真的到最后了，只有不是最后一个的情况可以那么做

代码：

<img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220219114003117.png" alt="image-20220219114003117" style="zoom: 67%;" />

使用链表可以让O(N)的空间复杂度变为O(1)

![image-20220509235110946](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220509235110946.png)

#### [117. 填充每个节点的下一个右侧节点指针 II](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/)

难度中等507

给定一个二叉树

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 `NULL`。

初始状态下，所有 next 指针都被设置为 `NULL`。

 

**进阶：**

- 你只能使用常量级额外空间。
- 使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。

 

**示例：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/02/15/117_sample.png)

```
输入：root = [1,2,3,4,5,null,7]
输出：[1,#,2,3,#,4,5,7,#]
解释：给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。序列化输出按层序遍历顺序（由 next 指针连接），'#' 表示每层的末尾
```

思路：

- 和上一题一模一样

代码：

<img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220219114841136.png" alt="image-20220219114841136" style="zoom:67%;" />

![image-20220510113532782](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220510113532782.png)

#### [104. 二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

难度简单1113

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明:** 叶子节点是指没有子节点的节点。

**示例：**
给定二叉树 `[3,9,20,null,null,15,7]`，

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。

思路：

注意`not root`，返回的是0，不是None

代码：

<img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220219120814769.png" alt="image-20220219120814769" style="zoom:67%;" />

> 559作为和104相似题，二刷做

#### [559. N 叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-n-ary-tree/)

难度简单251

给定一个 N 叉树，找到其最大深度。

最大深度是指从根节点到最远叶子节点的最长路径上的节点总数。

N 叉树输入按层序遍历序列化表示，每组子节点由空值分隔（请参见示例）。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png)

```
输入：root = [1,null,3,2,4,null,5,6]
输出：3
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2019/11/08/sample_4_964.png)

```
输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
输出：5
```

思路：



代码：

![image-20220510115005706](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220510115005706.png)



#### [111. 二叉树的最小深度](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

难度简单674

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

**说明：**叶子节点是指没有子节点的节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/12/ex_depth.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：2
```

**示例 2：**

```
输入：root = [2,null,3,null,4,null,5,null,6]
输出：5
```

思路：

- 不用想的太复杂，如果当前遇到左右孩子都为空，就停止
- 注意一开始的深度就是1
- 由于这里可能存在左边长，右边短，所以deque中把root的节点和深度绑定
- ![image-20220220234116131](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220220234116131.png)
- 注意deque()函数里面的样子，之前是[root], 现在是[(root, 1)], 或者[[root, 1]]
  - ![image-20220510120019632](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220510120019632.png)
  - ![image-20220510120029422](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220510120029422.png)
  - ![image-20220510120136853](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220510120136853.png)
  - ![image-20220510120151069](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220510120151069.png)

- 注意最后往que里面append还是要()

代码：

![image-20220220234524276](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220220234524276.png)

### 3.二叉树的属性

#### [101. 对称二叉树](https://leetcode-cn.com/problems/symmetric-tree/)

难度简单1746

给你一个二叉树的根节点 `root` ， 检查它是否轴对称。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg)

```
输入：root = [1,2,2,3,4,4,3]
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/02/19/symtree2.jpg)

```
输入：root = [1,2,2,null,3,null,3]
输出：false
```

思路：

- 这道题和之前一样，解决方法主要考虑递归和迭代，不过这里的迭代不再是层序遍历，只是单纯寻找个容器存储内容后进行遍历
- 首先是递归法
  - 迭代法永远都是内置一个新的函数
  - 我要解决的是什么？我递归的是什么？我递归的是两个节点的比较，是不是空，不空的话数值是不是相等。如果这两个点相等，我的下一层将是left的left和right的right，left的right和right的left
  - ![image-20220510134800756](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220510134800756.png)
- 然后是迭代法
  - 迭代法有两个选择，无非就是使用队列，也就是deque。或者是使用栈，就是单纯的[]。前者是popleft(), 后者是pop()
  - 虽然pop是从后面弹出，popleft是从左边弹出，但是压入都是成对压入，所以只要是相邻两个即可
  - 也就是按照left.left, right.right, left.right, right.left的顺序压入即可
  - 需要注意，发现两个都是空，不能像之前一样返回True，而是continue检查value
  - 队列
    ![image-20220510134213374](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220510134213374.png)
  - 堆栈
    <img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220222203247875.png" alt="image-20220222203247875" style="zoom:67%;" />
    <img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220222203311461.png" alt="image-20220222203311461" style="zoom:67%;" />

> 下面两道题100和572是作为和101相近的补充题，二刷的时候做

#### [100. 相同的树](https://leetcode-cn.com/problems/same-tree/)

难度简单765

给你两棵二叉树的根节点 `p` 和 `q` ，编写一个函数来检验这两棵树是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg)

```
输入：p = [1,2,3], q = [1,2,3]
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg)

```
输入：p = [1,2], q = [1,null,2]
输出：false
```

**示例 3：**

![img](https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg)

```
输入：p = [1,2,1], q = [1,1,2]
输出：false
```

思路：

代码：

Iteration:

![image-20220510142305605](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220510142305605.png)

Recursion:

![image-20220511124350274](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220511124350274.png)

![image-20220510142659365](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220510142659365.png)

#### [572. 另一棵树的子树](https://leetcode-cn.com/problems/subtree-of-another-tree/)

难度简单651

给你两棵二叉树 `root` 和 `subRoot` 。检验 `root` 中是否包含和 `subRoot` 具有相同结构和节点值的子树。如果存在，返回 `true` ；否则，返回 `false` 。

二叉树 `tree` 的一棵子树包括 `tree` 的某个节点和这个节点的所有后代节点。`tree` 也可以看做它自身的一棵子树。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/04/28/subtree1-tree.jpg)

```
输入：root = [3,4,5,1,2], subRoot = [4,1,2]
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/04/28/subtree2-tree.jpg)

```
输入：root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
输出：false
```

思路：

代码：

![image-20220511122659534](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220511122659534.png)

#### [222. 完全二叉树的节点个数](https://leetcode-cn.com/problems/count-complete-tree-nodes/)

难度中等618

给你一棵 **完全二叉树** 的根节点 `root` ，求出该树的节点个数。

[完全二叉树](https://baike.baidu.com/item/完全二叉树/7773232?fr=aladdin) 的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 `h` 层，则该层包含 `1~ 2h` 个节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/14/complete.jpg)

```
输入：root = [1,2,3,4,5,6]
输出：6
```

**示例 2：**

```
输入：root = []
输出：0
```

**示例 3：**

```
输入：root = [1]
输出：1
```

思路：

- 递归法

  - 时间复杂度：O(n)
  - 空间复杂度：O(logn)算上了递归系统栈占用的空间

- 迭代法

  - 时间复杂度：O(n)
  - 空间复杂度：O(n)

  - 还是使用层次遍历，加一个计数罢了

代码：

- 递归法

<img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220222212037595.png" alt="image-20220222212037595" style="zoom:67%;" />

- 迭代法
  
  <img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220222210701345.png" alt="image-20220222210701345" style="zoom:67%;" />
  
  但是上述的方法没有从complete binary tree这个消息中获利
  
  我们可以不计算前面的，因为他们必然是满的，只要知道最后一层有几个节点就可以知道全部的

![fic](https://leetcode.com/problems/count-complete-tree-nodes/Figures/222/level.png)

Now there are two questions:

1. How many nodes in the last level have to be checked?
2. What is the best time performance for such a check

需要check的node数目：

![pic](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/exist.png)

每次check的复杂度：

![pif](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/check.png)

![image-20220512203651779](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220512203651779.png)

记住node一定是都长在左边，我们要找到第一个没有的，也就是边界left，所以用二分查找

![image-20220512205553200](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220512205553200.png)

#### [110. 平衡二叉树](https://leetcode-cn.com/problems/balanced-binary-tree/)

难度简单891

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

> 一个二叉树*每个节点* 的左右两个子树的高度差的绝对值不超过 1 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/10/06/balance_2.jpg)

```
输入：root = [1,2,2,3,3,null,null,4,4]
输出：false
```

**示例 3：**

```
输入：root = []
输出：true
```

思路：

代码：

#### [257. 二叉树的所有路径](https://leetcode-cn.com/problems/binary-tree-paths/)

难度简单652

给你一个二叉树的根节点 `root` ，按 **任意顺序** ，返回所有从根节点到叶子节点的路径。

**叶子节点** 是指没有子节点的节点。

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/03/12/paths-tree.jpg)

```
输入：root = [1,2,3,null,5]
输出：["1->2->5","1->3"]
```

**示例 2：**

```
输入：root = [1]
输出：["1"]
```

思路：

代码：

#### [404. 左叶子之和](https://leetcode-cn.com/problems/sum-of-left-leaves/)

难度简单400

给定二叉树的根节点 `root` ，返回所有左叶子之和。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/04/08/leftsum-tree.jpg)

```
输入: root = [3,9,20,null,null,15,7] 
输出: 24 
解释: 在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24
```

**示例 2:**

```
输入: root = [1]
输出: 0
```

思路：

代码：

#### [513. 找树左下角的值](https://leetcode-cn.com/problems/find-bottom-left-tree-value/)

难度中等240

给定一个二叉树的 **根节点** `root`，请找出该二叉树的 **最底层 最左边** 节点的值。

假设二叉树中至少有一个节点。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2020/12/14/tree1.jpg)

```
输入: root = [2,1,3]
输出: 1
```

**示例 2:**

![img](https://assets.leetcode.com/uploads/2020/12/14/tree2.jpg)

```
输入: [1,2,3,4,null,5,6,null,null,7]
输出: 7
```

思路：

代码：

#### [112. 路径总和](https://leetcode-cn.com/problems/path-sum/)

难度简单787

给你二叉树的根节点 `root` 和一个表示目标和的整数 `targetSum` 。判断该树中是否存在 **根节点到叶子节点** 的路径，这条路径上所有节点值相加等于目标和 `targetSum` 。如果存在，返回 `true` ；否则，返回 `false` 。

**叶子节点** 是指没有子节点的节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsum1.jpg)

```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
输出：true
解释：等于目标和的根节点到叶节点路径如上图所示。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg)

```
输入：root = [1,2,3], targetSum = 5
输出：false
解释：树中存在两条根节点到叶子节点的路径：
(1 --> 2): 和为 3
(1 --> 3): 和为 4
不存在 sum = 5 的根节点到叶子节点的路径。
```

**示例 3：**

```
输入：root = [], targetSum = 0
输出：false
解释：由于树是空的，所以不存在根节点到叶子节点的路径。
```

思路：

代码：

#### [113. 路径总和 II](https://leetcode-cn.com/problems/path-sum-ii/)

难度中等671

给你二叉树的根节点 `root` 和一个整数目标和 `targetSum` ，找出所有 **从根节点到叶子节点** 路径总和等于给定目标和的路径。

**叶子节点** 是指没有子节点的节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsumii1.jpg)

```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg)

```
输入：root = [1,2,3], targetSum = 5
输出：[]
```

**示例 3：**

```
输入：root = [1,2], targetSum = 0
输出：[]
```

思路：

代码：

### 4.二叉树的改造和修改

#### [226. 翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)

难度简单1177

给你一棵二叉树的根节点 `root` ，翻转这棵二叉树，并返回其根节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg)

```
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/03/14/invert2-tree.jpg)

```
输入：root = [2,1,3]
输出：[2,3,1]
```

**示例 3：**

```
输入：root = []
输出：[]
```

思路：

- 本质就是每个节点下面的两个换一下位置，所以很容易想到迭代法
  - 先转换root下面的两个节点，再把这两个节点当作root进行迭代
- 迭代法就是把这些node存储在一个东西里面

代码：

- 递归法（前序遍历）
  - 使用前序遍历，就是中左右
  - ![image-20220221113958199](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220221113958199.png)
- 迭代法
- ![image-20220221114807652](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20220221114807652.png)

#### [106. 从中序与后序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

难度中等675

给定两个整数数组 `inorder` 和 `postorder` ，其中 `inorder` 是二叉树的中序遍历， `postorder` 是同一棵树的后序遍历，请你构造并返回这颗 *二叉树* 。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
输入：inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
输出：[3,9,20,null,null,15,7]
```

**示例 2:**

```
输入：inorder = [-1], postorder = [-1]
输出：[-1]
```

思路：

代码：

#### [105. 从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

难度中等1432

给定两个整数数组 `preorder` 和 `inorder` ，其中 `preorder` 是二叉树的**先序遍历**， `inorder` 是同一棵树的**中序遍历**，请构造二叉树并返回其根节点。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
输入: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
输出: [3,9,20,null,null,15,7]
```

**示例 2:**

```
输入: preorder = [-1], inorder = [-1]
输出: [-1]
```

思路：

代码：

#### [654. 最大二叉树](https://leetcode-cn.com/problems/maximum-binary-tree/)

难度中等372

给定一个不重复的整数数组 `nums` 。 **最大二叉树** 可以用下面的算法从 `nums` 递归地构建:

1. 创建一个根节点，其值为 `nums` 中的最大值。
2. 递归地在最大值 **左边** 的 **子数组前缀上** 构建左子树。
3. 递归地在最大值 **右边** 的 **子数组后缀上** 构建右子树。

返回 *`nums` 构建的* ***最大二叉树\*** 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/12/24/tree1.jpg)

```
输入：nums = [3,2,1,6,0,5]
输出：[6,3,5,null,2,0,null,null,1]
解释：递归调用如下所示：
- [3,2,1,6,0,5] 中的最大值是 6 ，左边部分是 [3,2,1] ，右边部分是 [0,5] 。
    - [3,2,1] 中的最大值是 3 ，左边部分是 [] ，右边部分是 [2,1] 。
        - 空数组，无子节点。
        - [2,1] 中的最大值是 2 ，左边部分是 [] ，右边部分是 [1] 。
            - 空数组，无子节点。
            - 只有一个元素，所以子节点是一个值为 1 的节点。
    - [0,5] 中的最大值是 5 ，左边部分是 [0] ，右边部分是 [] 。
        - 只有一个元素，所以子节点是一个值为 0 的节点。
        - 空数组，无子节点。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/12/24/tree2.jpg)

```
输入：nums = [3,2,1]
输出：[3,null,2,null,1]
```

思路：

代码：

#### [617. 合并二叉树](https://leetcode-cn.com/problems/merge-two-binary-trees/)

难度简单880

给你两棵二叉树： `root1` 和 `root2` 。

想象一下，当你将其中一棵覆盖到另一棵之上时，两棵树上的一些节点将会重叠（而另一些不会）。你需要将这两棵树合并成一棵新二叉树。合并的规则是：如果两个节点重叠，那么将这两个节点的值相加作为合并后节点的新值；否则，**不为** null 的节点将直接作为新二叉树的节点。

返回合并后的二叉树。

**注意:** 合并过程必须从两个树的根节点开始。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/05/merge.jpg)

```
输入：root1 = [1,3,2,5], root2 = [2,1,3,null,4,null,7]
输出：[3,4,5,5,4,null,7]
```

**示例 2：**

```
输入：root1 = [1], root2 = [1,2]
输出：[2,2]
```

思路：

代码：

#### [536. 从字符串生成二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-string/)

难度中等83

你需要用一个包括括号和整数的字符串构建一棵二叉树。

输入的字符串代表一棵二叉树。它包括整数和随后的 0 、1 或 2 对括号。整数代表根的值，一对括号内表示同样结构的子树。

若存在子结点，则从**左子结点**开始构建。

 

**示例 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/butree.jpg)

```
输入： s = "4(2(3)(1))(6(5))"
输出： [4,2,6,3,1,5]
```

**示例 2:**

```
输入： s = "4(2(3)(1))(6(5)(7))"
输出： [4,2,6,3,1,5,7]
```

**示例 3:**

```
输入： s = "-4(2(3)(1))(6(5)(7))"
输出： [-4,2,6,3,1,5,7]
```

 

**提示：**

- `0 <= s.length <= 3 * 104`
- 输入字符串中只包含 `'('`, `')'`, `'-'` 和 `'0'` ~ `'9'` 
- 空树由 `""` 而非`"()"`表示。

### 5.二叉搜索树的属性

#### [700. 二叉搜索树中的搜索](https://leetcode-cn.com/problems/search-in-a-binary-search-tree/)

难度简单242

给定二叉搜索树（BST）的根节点 `root` 和一个整数值 `val`。

你需要在 BST 中找到节点值等于 `val` 的节点。 返回以该节点为根的子树。 如果节点不存在，则返回 `null` 。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/01/12/tree1.jpg)

```
输入：root = [4,2,7,1,3], val = 2
输出：[2,1,3]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/01/12/tree2.jpg)

```
输入：root = [4,2,7,1,3], val = 5
输出：[]
```

#### [98. 验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)

难度中等1420

给你一个二叉树的根节点 `root` ，判断其是否是一个有效的二叉搜索树。

**有效** 二叉搜索树定义如下：

- 节点的左子树只包含 **小于** 当前节点的数。
- 节点的右子树只包含 **大于** 当前节点的数。
- 所有左子树和右子树自身必须也是二叉搜索树。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

```
输入：root = [2,1,3]
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg)

```
输入：root = [5,1,4,null,null,3,6]
输出：false
解释：根节点的值是 5 ，但是右子节点的值是 4 。
```

#### [530. 二叉搜索树的最小绝对差](https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst/)

难度简单308

给你一个二叉搜索树的根节点 `root` ，返回 **树中任意两不同节点值之间的最小差值** 。

差值是一个正数，其数值等于两值之差的绝对值。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/05/bst1.jpg)

```
输入：root = [4,2,6,1,3]
输出：1
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/02/05/bst2.jpg)

```
输入：root = [1,0,48,null,null,12,49]
输出：1
```

#### [501. 二叉搜索树中的众数](https://leetcode-cn.com/problems/find-mode-in-binary-search-tree/)

难度简单451

给你一个含重复值的二叉搜索树（BST）的根节点 `root` ，找出并返回 BST 中的所有 [众数](https://baike.baidu.com/item/众数/44796)（即，出现频率最高的元素）。

如果树中有不止一个众数，可以按 **任意顺序** 返回。

假定 BST 满足如下定义：

- 结点左子树中所含节点的值 **小于等于** 当前节点的值
- 结点右子树中所含节点的值 **大于等于** 当前节点的值
- 左子树和右子树都是二叉搜索树

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/mode-tree.jpg)

```
输入：root = [1,null,2,2]
输出：[2]
```

**示例 2：**

```
输入：root = [0]
输出：[0]
```

 

**提示：**

- 树中节点的数目在范围 `[1, 104]` 内
- `-105 <= Node.val <= 105`

 

**进阶：**你可以不使用额外的空间吗？（假设由递归产生的隐式调用栈的开销不被计算在内）



#### [538. 把二叉搜索树转换为累加树](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)

难度中等713

给出二叉 **搜索** 树的根节点，该树的节点值各不相同，请你将其转换为累加树（Greater Sum Tree），使每个节点 `node` 的新值等于原树中大于或等于 `node.val` 的值之和。

提醒一下，二叉搜索树满足下列约束条件：

- 节点的左子树仅包含键 **小于** 节点键的节点。
- 节点的右子树仅包含键 **大于** 节点键的节点。
- 左右子树也必须是二叉搜索树。

**注意：**本题和 1038: https://leetcode-cn.com/problems/binary-search-tree-to-greater-sum-tree/ 相同

 

**示例 1：**

**![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/tree.png)**

```
输入：[4,1,6,0,2,5,7,null,null,null,3,null,null,null,8]
输出：[30,36,21,36,35,26,15,null,null,null,33,null,null,null,8]
```

**示例 2：**

```
输入：root = [0,null,1]
输出：[1,null,1]
```

**示例 3：**

```
输入：root = [1,0,2]
输出：[3,3,2]
```

**示例 4：**

```
输入：root = [3,2,4,1]
输出：[7,9,4,10]
```

 

**提示：**

- 树中的节点数介于 `0` 和 `104` 之间。
- 每个节点的值介于 `-104` 和 `104` 之间。
- 树中的所有值 **互不相同**。
- 给定的树为二叉搜索树

### 6. 二叉树的公共祖先

#### [235. 二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

难度简单829

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

[百度百科](https://baike.baidu.com/item/最近公共祖先/8918834?fr=aladdin)中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（**一个节点也可以是它自己的祖先**）。”

例如，给定如下二叉搜索树: root = [6,2,8,0,4,7,9,null,null,3,5]

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/binarysearchtree_improved.png)

 

**示例 1:**

```
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
输出: 6 
解释: 节点 2 和节点 8 的最近公共祖先是 6。
```

**示例 2:**

```
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
输出: 2
解释: 节点 2 和节点 4 的最近公共祖先是 2, 因为根据定义最近公共祖先节点可以为节点本身。
```

 

**说明:**

- 所有节点的值都是唯一的。
- p、q 为不同节点且均存在于给定的二叉搜索树中。

#### [236. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

难度中等1731

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

[百度百科](https://baike.baidu.com/item/最近公共祖先/8918834?fr=aladdin)中最近公共祖先的定义为：“对于有根树 T 的两个节点 p、q，最近公共祖先表示为一个节点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（**一个节点也可以是它自己的祖先**）。”

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
输入：root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
输出：3
解释：节点 5 和节点 1 的最近公共祖先是节点 3 。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
输入：root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
输出：5
解释：节点 5 和节点 4 的最近公共祖先是节点 5 。因为根据定义最近公共祖先节点可以为节点本身。
```

**示例 3：**

```
输入：root = [1,2], p = 1, q = 2
输出：1
```

 

**提示：**

- 树中节点数目在范围 `[2, 105]` 内。
- `-109 <= Node.val <= 109`
- 所有 `Node.val` `互不相同` 。
- `p != q`
- `p` 和 `q` 均存在于给定的二叉树中。

### 7. 二叉搜索树的修改和构造

#### [701. 二叉搜索树中的插入操作](https://leetcode-cn.com/problems/insert-into-a-binary-search-tree/)

难度中等304

给定二叉搜索树（BST）的根节点 `root` 和要插入树中的值 `value` ，将值插入二叉搜索树。 返回插入后二叉搜索树的根节点。 输入数据 **保证** ，新值和原始二叉搜索树中的任意节点值都不同。

**注意**，可能存在多种有效的插入方式，只要树在插入后仍保持为二叉搜索树即可。 你可以返回 **任意有效的结果** 。

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/insertbst.jpg)

```
输入：root = [4,2,7,1,3], val = 5
输出：[4,2,7,1,3,5]
解释：另一个满足题目要求可以通过的树是：
```

**示例 2：**

```
输入：root = [40,20,60,10,30,50,70], val = 25
输出：[40,20,60,10,30,50,70,null,null,25]
```

**示例 3：**

```
输入：root = [4,2,7,1,3,null,null,null,null,null,null], val = 5
输出：[4,2,7,1,3,5]
```

 

**提示：**

- 树中的节点数将在 `[0, 104]`的范围内。
- `-108 <= Node.val <= 108`
- 所有值 `Node.val` 是 **独一无二** 的。
- `-108 <= val <= 108`
- **保证** `val` 在原始BST中不存在。

#### [450. 删除二叉搜索树中的节点](https://leetcode-cn.com/problems/delete-node-in-a-bst/)

难度中等738

给定一个二叉搜索树的根节点 **root** 和一个值 **key**，删除二叉搜索树中的 **key** 对应的节点，并保证二叉搜索树的性质不变。返回二叉搜索树（有可能被更新）的根节点的引用。

一般来说，删除节点可分为两个步骤：

1. 首先找到需要删除的节点；
2. 如果找到了，删除它。

 

**示例 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/del_node_1.jpg)

```
输入：root = [5,3,6,2,4,null,7], key = 3
输出：[5,4,6,2,null,null,7]
解释：给定需要删除的节点值是 3，所以我们首先找到 3 这个节点，然后删除它。
一个正确的答案是 [5,4,6,2,null,null,7], 如下图所示。
另一个正确答案是 [5,2,6,null,4,null,7]。
```

**示例 2:**

```
输入: root = [5,3,6,2,4,null,7], key = 0
输出: [5,3,6,2,4,null,7]
解释: 二叉树不包含值为 0 的节点
```

**示例 3:**

```
输入: root = [], key = 0
输出: []
```

 

**提示:**

- 节点数的范围 `[0, 104]`.
- `-105 <= Node.val <= 105`
- 节点值唯一
- `root` 是合法的二叉搜索树
- `-105 <= key <= 105`

 

**进阶：** 要求算法时间复杂度为 O(h)，h 为树的高度。

#### [776. 拆分二叉搜索树](https://leetcode-cn.com/problems/split-bst/)

难度中等109

给你一棵二叉搜索树（BST）的根结点 `root` 和一个整数 `target` 。请将该树按要求拆分为两个子树：其中一个子树结点的值都必须小于等于给定的目标值；另一个子树结点的值都必须大于目标值；树中并非一定要存在值为 `target` 的结点。

除此之外，树中大部分结构都需要保留，也就是说原始树中父节点 `p` 的任意子节点 `c` ，假如拆分后它们仍在同一个子树中，那么结点 `p` 应仍为 `c` 的父结点。

返回 *两个子树的根结点的数组* 。

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/split-tree.jpg)

```
输入：root = [4,2,6,1,3,5,7], target = 2
输出：[[2,1],[4,3,6,null,null,5,7]]
```

**示例 2:**

```
输入: root = [1], target = 1
输出: [[1],[]]
```

 

**提示：**

- 二叉搜索树节点个数在 `[1, 50]` 范围内
- `0 <= Node.val, target <= 1000`

#### [669. 修剪二叉搜索树](https://leetcode-cn.com/problems/trim-a-binary-search-tree/)

难度中等530

给你二叉搜索树的根节点 `root` ，同时给定最小边界`low` 和最大边界 `high`。通过修剪二叉搜索树，使得所有节点的值在`[low, high]`中。修剪树 **不应该** 改变保留在树中的元素的相对结构 (即，如果没有被移除，原有的父代子代关系都应当保留)。 可以证明，存在 **唯一的答案** 。

所以结果应当返回修剪好的二叉搜索树的新的根节点。注意，根节点可能会根据给定的边界发生改变。

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/trim1.jpg)

```
输入：root = [1,0,2], low = 1, high = 2
输出：[1,null,2]
```

**示例 2：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/trim2.jpg)

```
输入：root = [3,0,4,null,2,null,null,1], low = 1, high = 3
输出：[3,2,null,1]
```

 

**提示：**

- 树中节点数在范围 `[1, 104]` 内
- `0 <= Node.val <= 104`
- 树中每个节点的值都是 **唯一** 的
- 题目数据保证输入是一棵有效的二叉搜索树
- `0 <= low <= high <= 104`

#### [108. 将有序数组转换为二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)

难度简单1030

给你一个整数数组 `nums` ，其中元素已经按 **升序** 排列，请你将其转换为一棵 **高度平衡** 二叉搜索树。

**高度平衡** 二叉树是一棵满足「每个节点的左右两个子树的高度差的绝对值不超过 1 」的二叉树。

 

**示例 1：**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/btree1.jpg)

```
输入：nums = [-10,-3,0,5,9]
输出：[0,-3,9,-10,null,5]
解释：[0,-10,5,null,-3,null,9] 也将被视为正确答案：
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/02/18/btree.jpg)

```
输入：nums = [1,3]
输出：[3,1]
解释：[1,null,3] 和 [3,1] 都是高度平衡二叉搜索树。
```

 

**提示：**

- `1 <= nums.length <= 104`
- `-104 <= nums[i] <= 104`
- `nums` 按 **严格递增** 顺序排列