---
layout:     post
title:      Stack & Queue (Updating)
subtitle:   
date:       2022-03-30
author:     Ethan
header-img: img/city_9.jpg
catalog: true
tags:
    - Leetcode
    - Stack
    - Queue

---

## 队列和栈

- 队列是先进先出

- 栈是先进后出



#### [232. 用栈实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

[^尝试用deque实现]: 

难度简单524

请你仅使用两个栈实现先入先出队列。队列应当支持一般队列支持的所有操作（`push`、`pop`、`peek`、`empty`）：

实现 `MyQueue` 类：

- `void push(int x)` 将元素 x 推到队列的末尾
- `int pop()` 从队列的开头移除并返回元素
- `int peek()` 返回队列开头的元素
- `boolean empty()` 如果队列为空，返回 `true` ；否则，返回 `false`

**说明：**

- 你只能使用标准的栈操作 —— 也就是只有 `push to top`, `peek/pop from top`, `size`, 和 `is empty` 操作是合法的。
- 你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。

 

**进阶：**

- 你能否实现每个操作均摊时间复杂度为 `O(1)` 的队列？换句话说，执行 `n` 个操作的总时间复杂度为 `O(n)` ，即使其中一个操作可能花费较长时间。

 

**示例：**

```
输入：
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
输出：
[null, null, null, 1, 1, false]

解释：
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
```

------

思路：

- 使用两个栈，一个作为输出栈，一个作为输入栈

  - 输入栈负责push
  - 输出栈负责pop和peek。每次需要输出的时候，输入栈将所有的内容pop到输出栈，这时输出栈里面是反向的

- 首先是最简单的empty，只要看两个栈是不是空的判断

- python的list的append符合push的功能，在list的末尾加上元素。所以对于push，只要在输入栈后面加上append(x)

- 至于pop，需要考虑的是当前输出栈里面是不是空的

  - 如果是空的，将当前的输入栈内容pop进来
  - 如果非空，pop输出栈的第一个内容，使用的是python自带的pop，他会返回list末尾元素

- 而peak可以服用pop，再把pop的元素push到stack_out

- 初始化init时，别忘了self

  而之后提及这两个，也别忘加self

  此外，之后调用功能，比如empty，也要self！
  ![image-20211228163615659](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20211228163615659.png)

- empty也有问题，但是没太理解
  ![image-20211228164822733](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20211228164822733.png)

- <img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20211228183311419.png" alt="image-20211228183311419" style="zoom:15%;" />

代码：

![image-20211228164837818](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20211228164837818.png)

![image-20211228164900984](C:\Users\BenWong\AppData\Roaming\Typora\typora-user-images\image-20211228164900984.png)

#### [225. 用队列实现栈](https://leetcode-cn.com/problems/implement-stack-using-queues/)

难度简单420

请你仅使用两个队列实现一个后入先出（LIFO）的栈，并支持普通栈的全部四种操作（`push`、`top`、`pop` 和 `empty`）。

实现 `MyStack` 类：

- `void push(int x)` 将元素 x 压入栈顶。
- `int pop()` 移除并返回栈顶元素。
- `int top()` 返回栈顶元素。
- `boolean empty()` 如果栈是空的，返回 `true` ；否则，返回 `false` 。

 

**注意：**

- 你只能使用队列的基本操作 —— 也就是 `push to back`、`peek/pop from front`、`size` 和 `is empty` 这些操作。
- 你所使用的语言也许不支持队列。 你可以使用 list （列表）或者 deque（双端队列）来模拟一个队列 , 只要是标准的队列操作即可。

 

**示例：**

```
输入：
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
输出：
[null, null, null, 2, 2, false]

解释：
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // 返回 2
myStack.pop(); // 返回 2
myStack.empty(); // 返回 False
```

------

思路:

- 需要使用到python的deque，也就是双向队列来完成
  - 它的操作很像list 同时相比于list实现的队列，deque实现拥有更低的时间和空间复杂度。
  - list实现在出队（pop）和插入（insert）时的空间复杂度大约为O(n)，deque在出队（pop）和入队（append）时的时间复杂度是O(1)。
  - <img src="https://img2020.cnblogs.com/i-beta/1959611/202003/1959611-20200307215621460-1733987446.png" alt="img" style="zoom: 67%;" />
  - <img src="C:\Users\ethan\AppData\Roaming\Typora\typora-user-images\image-20211228182210511.png" alt="image-20211228182210511" style="zoom: 50%;" />
  - deque的内部还是list，所以append和pop都可以操作，都是末尾的。对于左边的，可以使用popleft和appendleft。而这道题，我们只是模拟基础的队列，所以我们用且只会用到append和popleft
- 首先是push操作，就是对于queue_in进行append
- 然后是empty，可以使用和之前一样的写法，区别在于这里只用关注in
  - ![image-20211228185342526](C:\Users\ethan\AppData\Roaming\Typora\typora-user-images\image-20211228185342526.png)
  - 但是不能是==[], 而必须是长度 ==0
- 然后是pop，对于queue_in，先popleft到只剩下一个后，和queue_out进行交换，然后queue_out再popleft。
  - 我们可以看到，queue_out是一直保持空的状态，所以，empty只需要关于queue_in即可
- 最后是top，top要出去的是栈顶，但是queue没有pop，只有popleft。所以我们使用deque的索引，找到queue_in的最后一位
- <img src="C:\Users\ethan\AppData\Roaming\Typora\typora-user-images\image-20211228183217248.png" alt="image-20211228183217248" style="zoom: 15%;" />

代码:

![image-20211228185429417](C:\Users\eTHAN\AppData\Roaming\Typora\typora-user-images\image-20211228185429417.png)

![image-20211228185442972](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20211228185442972.png)

#### [20. 有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

难度简单2853

给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串 `s` ，判断字符串是否有效。

有效字符串需满足：

1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。

 

**示例 1：**

```
输入：s = "()"
输出：true
```

**示例 2：**

```
输入：s = "()[]{}"
输出：true
```

**示例 3：**

```
输入：s = "(]"
输出：false
```

**示例 4：**

```
输入：s = "([)]"
输出：false
```

**示例 5：**

```
输入：s = "{[]}"
输出：true
```

------

思路：

- 首先思考什么情况下会是False
  - 左边的括号多了
  - 右边的括号多了
  - 左边和右边匹配不上
- 使用栈来存储左侧括号，如果匹配，从栈的尾部pop出去
  - 第一个False，对应遍历完但是栈仍然非空
  - 第二个False，对应栈空了，但是没有遍历完
  - 第三个False，单纯不匹配
- 具体实现上，对于左括号的三种形式（{[, 如果匹配，在stack中存入他们的对偶形式。当发现不是这三种，也就是不是左括号时，看stack[-1],和输入中的元素是否一样。
  - 如果一样，把stack末尾pop
  - 如果不一样return False
  - 如果这个时候stack为空，但是输入还是有的，return False
- 上面是对输入遍历，如果遍历完输入，stack非空，return False

代码：

![image-20211229175316595](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20211229175316595.png)

#### [1047. 删除字符串中的所有相邻重复项](https://leetcode-cn.com/problems/remove-all-adjacent-duplicates-in-string/)

难度简单310

给出由小写字母组成的字符串 `S`，**重复项删除操作**会选择两个相邻且相同的字母，并删除它们。

在 S 上反复执行重复项删除操作，直到无法继续删除。

在完成所有重复项删除操作后返回最终的字符串。答案保证唯一。

思路：

- 和上一题很相似，使用栈来存储，再进行匹配判断，如果匹配，就pop，栈中剩下的作为输出
- 输出结果要用“”.join()

代码：

![image-20211229181715495](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20211229181715495.png)



**示例：**

```
输入："abbaca"
输出："ca"
解释：
例如，在 "abbaca" 中，我们可以删除 "bb" 由于两字母相邻且相同，这是此时唯一可以执行删除操作的重复项。之后我们得到字符串 "aaca"，其中又只有 "aa" 可以执行重复项删除操作，所以最后的字符串为 "ca"。
```

#### [150. 逆波兰表达式求值](https://leetcode-cn.com/problems/evaluate-reverse-polish-notation/)

难度中等438

根据[ 逆波兰表示法](https://baike.baidu.com/item/逆波兰式/128437)，求表达式的值。

有效的算符包括 `+`、`-`、`*`、`/` 。每个运算对象可以是整数，也可以是另一个逆波兰表达式。

 

**说明：**

- 整数除法只保留整数部分。
- 给定逆波兰表达式总是有效的。换句话说，表达式总会得出有效数值且不存在除数为 0 的情况。

 

**示例 1：**

```
输入：tokens = ["2","1","+","3","*"]
输出：9
解释：该算式转化为常见的中缀算术表达式为：((2 + 1) * 3) = 9
```

**示例 2：**

```
输入：tokens = ["4","13","5","/","+"]
输出：6
解释：该算式转化为常见的中缀算术表达式为：(4 + (13 / 5)) = 6
```

**示例 3：**

```
输入：tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
输出：22
解释：
该算式转化为常见的中缀算术表达式为：
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

思路：

- 使用栈解决，把数字存储到stack里面，一旦遇到符号，把栈后两位pop出来，进行运算，把结果放回栈

代码：

![image-20211229204332424](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20211229204332424.png)

![image-20211229204348197](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20211229204348197.png)

#### [239. 滑动窗口最大值](https://leetcode-cn.com/problems/sliding-window-maximum/)

难度困难1325

给你一个整数数组 `nums`，有一个大小为 `k` 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 `k` 个数字。滑动窗口每次只向右移动一位。

返回滑动窗口中的最大值。

 

**示例 1：**

```
输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
输出：[3,3,5,5,6,7]
解释：
滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**示例 2：**

```
输入：nums = [1], k = 1
输出：[1]
```

**示例 3：**

```
输入：nums = [1,-1], k = 1
输出：[1,-1]
```

**示例 4：**

```
输入：nums = [9,11], k = 2
输出：[11]
```

**示例 5：**

```
输入：nums = [4,-2], k = 2
输出：[4]
```

思路：

- 使用的方法是单调队列：同时弹出队首和队尾的元素是双端队列。满足这种单调性的双端队列一般称作「单调队列」。这里的单调性是队列中存储的是位置，位置对应的数字是单调递减的

- 随着窗口滑动，会有一个新的元素进来.

  - 如果新的元素比队尾元素小，nums[i] <nums[queue[-1]], 则存入队列，
  - 如果比队尾元素大或一样，则将队尾元素pop出去，直到发现有一个队列中元素比他大，或者他来到了队列最前端。
  - 对于前k个可以这么做来找到queue[0]，存储到ans中

- 对于k到n，此时每滑动一次都要将queue[0]对应的值放入ans

  - 相比起前k个。需要额外考虑的是：万一一直是最先进来的元素最大，比如[5,4,3,2,1],那么首部将不会被赶走。所以需要不断看当前queue中第一位所存储的位置是否满足queue[0]>i-k，如果不满足需要popleft把头部去掉

- 注意，生成第一个queue的元素，要经历好几次pop。所以不能分开来，要在一个while里面：
  ![image-20211229234910996](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20211229234910996.png)

  ![image-20211229235256929](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20211229235256929.png)

代码：

![image-20211229235235768](C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20211229235235768.png)

#### [347. 前 K 个高频元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)

难度中等961

给你一个整数数组 `nums` 和一个整数 `k` ，请你返回其中出现频率前 `k` 高的元素。你可以按 **任意顺序** 返回答案。

 

**示例 1:**

```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```

**示例 2:**

```
输入: nums = [1], k = 1
输出: [1]
```

思路：

- 三件事情，计算并存储频率，频率比较，拿出前k个高频的

- 对于计算并且存储频率，使用Python字典实现hashmap，使用hashmap存储每个数字的频率。

  - 使用Python 字典get() 函数返回指定键的值

  - ```
    dict.get(key, default=None)
    ```

  - key -- 字典中要查找的键。

  - default -- 如果指定的键不存在时，返回该默认值。

  - 根据每个key，不断查询该key的出现频率，并进行更新

  - ![image-20211230074024782](C:\Users\BenWong\AppData\Roaming\Typora\typora-user-images\image-20211230074024782.png)

- 对于频率比较，使用优先队列。

  - 这里使用heapq模块来进行堆操作。堆（heap）是一种优先队列。优先队列让你能够以任意顺序添加对象，并随时找出（并删除）最小的元素。相比于列表方法min，这样做的效率要高得多。
  - <img src="C:\Users\BenWong\AppData\Roaming\Typora\typora-user-images\image-20211208182112339.png" alt="image-20211208182112339" style="zoom:50%;" />
  - 创建`heap=[]`。然后将刚才得到的键值对压入heap中，注意压入负值，即负的频率。这样到时候pop出来的就是从大到小的顺序。
  - 此外，需要注意遍历heapmap的`key, value`的时候要加`.items()`
  - ![image-20211230074226562](C:\Users\BenWong\AppData\Roaming\Typora\typora-user-images\image-20211230074226562.png)

- 最后是前k个，进行`heappop(heap)[1]`。heappop得到的是最前面的，是负的最厉害的频率，也就是最大频率。[1]是他对于的键，因为heap里面存的是-value和key

**代码：**

<img src="C:\Users\BenWong\AppData\Roaming\Typora\typora-user-images\image-20211208184305119.png" alt="image-20211208184305119" style="zoom:50%;" />

##### 



#### [155. 最小栈](https://leetcode-cn.com/problems/min-stack/)

难度简单1124

设计一个支持 `push` ，`pop` ，`top` 操作，并能在常数时间内检索到最小元素的栈。

- `push(x)` —— 将元素 x 推入栈中。
- `pop()` —— 删除栈顶的元素。
- `top()` —— 获取栈顶元素。
- `getMin()` —— 检索栈中的最小元素。

 

**示例:**

```
输入：
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

输出：
[null,null,null,null,-3,null,0,-2]

解释：
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2
```

## 单调栈

#### [739. Daily Temperatures](https://leetcode-cn.com/problems/daily-temperatures/)

难度中等1085

Given an array of integers `temperatures` represents the daily temperatures, return *an array* `answer` *such that* `answer[i]` *is the number of days you have to wait after the* `ith` *day to get a warmer temperature*. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

 

**Example 1:**

```
Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
```

**Example 2:**

```
Input: temperatures = [30,40,50,60]
Output: [1,1,1,0]
```

**Example 3:**

```
Input: temperatures = [30,60,90]
Output: [1,1,0]
```

#### [496. Next Greater Element I](https://leetcode-cn.com/problems/next-greater-element-i/)

难度简单679

The **next greater element** of some element `x` in an array is the **first greater** element that is **to the right** of `x` in the same array.

You are given two **distinct 0-indexed** integer arrays `nums1` and `nums2`, where `nums1` is a subset of `nums2`.

For each `0 <= i < nums1.length`, find the index `j` such that `nums1[i] == nums2[j]` and determine the **next greater element** of `nums2[j]` in `nums2`. If there is no next greater element, then the answer for this query is `-1`.

Return *an array* `ans` *of length* `nums1.length` *such that* `ans[i]` *is the **next greater element** as described above.*

 

**Example 1:**

```
Input: nums1 = [4,1,2], nums2 = [1,3,4,2]
Output: [-1,3,-1]
Explanation: The next greater element for each value of nums1 is as follows:
- 4 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
- 1 is underlined in nums2 = [1,3,4,2]. The next greater element is 3.
- 2 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
```

**Example 2:**

```
Input: nums1 = [2,4], nums2 = [1,2,3,4]
Output: [3,-1]
Explanation: The next greater element for each value of nums1 is as follows:
- 2 is underlined in nums2 = [1,2,3,4]. The next greater element is 3.
- 4 is underlined in nums2 = [1,2,3,4]. There is no next greater element, so the answer is -1.
```

#### [503. Next Greater Element II](https://leetcode-cn.com/problems/next-greater-element-ii/)

难度中等588

Given a circular integer array `nums` (i.e., the next element of `nums[nums.length - 1]` is `nums[0]`), return *the **next greater number** for every element in* `nums`.

The **next greater number** of a number `x` is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, return `-1` for this number.

 

**Example 1:**

```
Input: nums = [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number. 
The second 1's next greater number needs to search circularly, which is also 2.
```

**Example 2:**

```
Input: nums = [1,2,3,4,3]
Output: [2,3,4,-1,4]
```

#### [42. Trapping Rain Water](https://leetcode-cn.com/problems/trapping-rain-water/)

难度困难3306

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/rainwatertrap.png)

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```

**Example 2:**

```
Input: height = [4,2,0,3,2,5]
Output: 9
```

#### [84. Largest Rectangle in Histogram](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)

难度困难1855

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return *the area of the largest rectangle in the histogram*.

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/histogram.jpg)

```
Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/histogram-1.jpg)

```
Input: heights = [2,4]
Output: 4
```