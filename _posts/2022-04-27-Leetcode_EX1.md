---
layout:     post
title:      Exercise 1
subtitle:   
date:       2022-04-26
author:     Ethan
header-img: img/2.jpg
catalog: true
tags:
    - Leetcode
---

## Exercise 1 (12题)

#### [273. Integer to English Words](https://leetcode-cn.com/problems/integer-to-english-words/)

难度困难268

Convert a non-negative integer `num` to its English words representation.

 

**Example 1:**

```
Input: num = 123
Output: "One Hundred Twenty Three"
```

**Example 2:**

```
Input: num = 12345
Output: "Twelve Thousand Three Hundred Forty Five"
```

**Example 3:**

```
Input: num = 1234567
Output: "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```

 

**Constraints:**

- `0 <= num <= 231 - 1`

#### [253. Meeting Rooms II](https://leetcode-cn.com/problems/meeting-rooms-ii/)

难度中等427

Given an array of meeting time intervals `intervals` where `intervals[i] = [starti, endi]`, return *the minimum number of conference rooms required*.

 

**Example 1:**

```
Input: intervals = [[0,30],[5,10],[15,20]]
Output: 2
```

**Example 2:**

```
Input: intervals = [[7,10],[2,4]]
Output: 1
```

 

**Constraints:**

- `1 <= intervals.length <= 104`
- `0 <= starti < endi <= 106`

通过次数45,705

提交次数89,140



#### [1010. Pairs of Songs With Total Durations Divisible by 60](https://leetcode-cn.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/)

难度中等178

You are given a list of songs where the `ith` song has a duration of `time[i]` seconds.

Return *the number of pairs of songs for which their total duration in seconds is divisible by* `60`. Formally, we want the number of indices `i`, `j` such that `i < j` with `(time[i] + time[j]) % 60 == 0`.

 

**Example 1:**

```
Input: time = [30,20,150,100,40]
Output: 3
Explanation: Three pairs have a total duration divisible by 60:
(time[0] = 30, time[2] = 150): total duration 180
(time[1] = 20, time[3] = 100): total duration 120
(time[1] = 20, time[4] = 40): total duration 60
```

**Example 2:**

```
Input: time = [60,60,60]
Output: 3
Explanation: All three pairs have a total duration of 120, which is divisible by 60.
```

 

**Constraints:**

- `1 <= time.length <= 6 * 104`
- `1 <= time[i] <= 500`

思路：

- 最显然的方法是brute force，两层for循环
- 时间复杂度是O(N*2), 空间复杂度是O(1)
- 一开始在想双指针，但显然不是
- 事实上是hash table和一些数学想法，主要是求模的思想
- ![image-20220504135518390](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504135518390.png)
- 如果a和b的和与60求模是0；那么a和b单独和60求模的和在和60求模也是0
- 一个关键点是hash table不是存每个time，而是time%60后的结果
- 分离a和b都是可以mod 60是为了排除hash table[0] and hash table[60]的冲突
  - 因为else使用的是互补的逻辑，用60来减i%60
  - ![image-20220504140518299](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504140518299.png)
- 使用defaultdict()而不是一般的dict()来保证初始就是0。注意要写入类型是int才会是0
  - ![image-20220504140307777](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504140307777.png)
- 第十三行，每次结束要加一，别忘了！面试要注意细节

代码：

![image-20220504140609891](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504140609891.png)

- 时间复杂度O(N), 空间复杂度O(1)

#### [636. Exclusive Time of Functions](https://leetcode-cn.com/problems/exclusive-time-of-functions/)

难度中等153

On a **single-threaded** CPU, we execute a program containing `n` functions. Each function has a unique ID between `0` and `n-1`.

Function calls are **stored in a [call stack](https://en.wikipedia.org/wiki/Call_stack)**: when a function call starts, its ID is pushed onto the stack, and when a function call ends, its ID is popped off the stack. The function whose ID is at the top of the stack is **the current function being executed**. Each time a function starts or ends, we write a log with the ID, whether it started or ended, and the timestamp.

You are given a list `logs`, where `logs[i]` represents the `ith` log message formatted as a string `"{function_id}:{"start" | "end"}:{timestamp}"`. For example, `"0:start:3"` means a function call with function ID `0` **started at the beginning** of timestamp `3`, and `"1:end:2"` means a function call with function ID `1` **ended at the end** of timestamp `2`. Note that a function can be called **multiple times, possibly recursively**.

A function's **exclusive time** is the sum of execution times for all function calls in the program. For example, if a function is called twice, one call executing for `2` time units and another call executing for `1` time unit, the **exclusive time** is `2 + 1 = 3`.

Return *the **exclusive time** of each function in an array, where the value at the* `ith` *index represents the exclusive time for the function with ID* `i`.

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/diag1b.png)

```
Input: n = 2, logs = ["0:start:0","1:start:2","1:end:5","0:end:6"]
Output: [3,4]
Explanation:
Function 0 starts at the beginning of time 0, then it executes 2 for units of time and reaches the end of time 1.
Function 1 starts at the beginning of time 2, executes for 4 units of time, and ends at the end of time 5.
Function 0 resumes execution at the beginning of time 6 and executes for 1 unit of time.
So function 0 spends 2 + 1 = 3 units of total time executing, and function 1 spends 4 units of total time executing.
```

**Example 2:**

```
Input: n = 1, logs = ["0:start:0","0:start:2","0:end:5","0:start:6","0:end:6","0:end:7"]
Output: [8]
Explanation:
Function 0 starts at the beginning of time 0, executes for 2 units of time, and recursively calls itself.
Function 0 (recursive call) starts at the beginning of time 2 and executes for 4 units of time.
Function 0 (initial call) resumes execution then immediately calls itself again.
Function 0 (2nd recursive call) starts at the beginning of time 6 and executes for 1 unit of time.
Function 0 (initial call) resumes execution at the beginning of time 7 and executes for 1 unit of time.
So function 0 spends 2 + 4 + 1 + 1 = 8 units of total time executing.
```

**Example 3:**

```
Input: n = 2, logs = ["0:start:0","0:start:2","0:end:5","1:start:6","1:end:6","0:end:7"]
Output: [7,1]
Explanation:
Function 0 starts at the beginning of time 0, executes for 2 units of time, and recursively calls itself.
Function 0 (recursive call) starts at the beginning of time 2 and executes for 4 units of time.
Function 0 (initial call) resumes execution then immediately calls function 1.
Function 1 starts at the beginning of time 6, executes 1 unit of time, and ends at the end of time 6.
Function 0 resumes execution at the beginning of time 6 and executes for 2 units of time.
So function 0 spends 2 + 4 + 1 = 7 units of total time executing, and function 1 spends 1 unit of total time executing.
```

 

**Constraints:**

- `1 <= n <= 100`
- `1 <= logs.length <= 500`
- `0 <= function_id < n`
- `0 <= timestamp <= 109`
- No two start events will happen at the same timestamp.
- No two end events will happen at the same timestamp.
- Each function has an `"end"` log for each `"start"` log.

#### [1152. 用户网站访问行为分析](https://leetcode-cn.com/problems/analyze-user-website-visit-pattern/)

难度中等18

给定两个字符串数组 `username` 和 `website` 和一个整数数组 `timestamp` 。给定的数组长度相同，其中元组 `[username[i], website[i], timestamp[i]]` 表示用户 `username[i]` 在时间 `timestamp[i]` 访问了网站 `website[i]` 。

**访问模式** 是包含三个网站的列表(不一定是完全不同的)。

- 例如，`["home"， "away"， "love"]`， `["leetcode"， "love"， "leetcode"]`，和 `["luffy"， "luffy"， "luffy"]` 都是模式。

一种 **访问****模式** 的 **得分** 是访问该模式中所有网站的用户数量，这些网站在该模式中出现的顺序相同。

- 例如，如果模式是 `[“home”，“away”，“love”] `，那么分数就是用户数量 `x` , `x` 访问了 “`home”` ，然后访问了 `“away”` ，然后访问了 `“love” `。
- 同样，如果模式是 `["leetcode"， "love"， "leetcode"]` ，那么分数就是用户数量 `x` ，使得 `x` 访问了`"leetcode"`，然后访问了 `"love"` ，之后又访问了 `"leetcode"` 。
- 另外，如果模式是 `[“luffy”，“luffy”，“luffy”]` ，那么分数就是用户数量 `x` ，这样 `x` 就可以在不同的时间戳上访问 `“luffy”` 三次。

返回 ***得分** 最大的 **访问****模式*** 。如果有多个访问模式具有相同的最大分数，则返回字典序最小的。

 

**示例 1：**

```
输入：username = ["joe","joe","joe","james","james","james","james","mary","mary","mary"], timestamp = [1,2,3,4,5,6,7,8,9,10], website = ["home","about","career","home","cart","maps","home","home","about","career"]
输出：["home","about","career"]
解释：本例中的元组是:
["joe","home",1],["joe","about",2],["joe","career",3],["james","home",4],["james","cart",5],["james","maps",6],["james","home",7],["mary","home",8],["mary","about",9], and ["mary","career",10].
模式("home", "about", "career") has score 2 (joe and mary).
模式("home", "cart", "maps") 的得分为 1 (james).
模式 ("home", "cart", "home") 的得分为 1 (james).
模式 ("home", "maps", "home") 的得分为 1 (james).
模式 ("cart", "maps", "home") 的得分为 1 (james).
模式 ("home", "home", "home") 的得分为 0(没有用户访问过home 3次)。
```

**示例 2：**

```
输入: username = ["ua","ua","ua","ub","ub","ub"], timestamp = [1,2,3,4,5,6], website = ["a","b","a","a","b","c"]
输出: ["a","b","a"]
```

 

**提示：**

- `3 <= username.length <= 50`
- `1 <= username[i].length <= 10`
- `timestamp.length == username.length`
- `1 <= timestamp[i] <= 109`
- `website.length == username.length`
- `1 <= website[i].length <= 10`
- `username[i]` 和 `website[i]` 都只含小写字符
- 它保证至少有一个用户访问了至少三个网站
- 所有元组 `[username[i]， timestamp[i]， website[i]` 均 **不重复**

#### [716. Max Stack](https://leetcode-cn.com/problems/max-stack/)

难度简单101

Design a max stack data structure that supports the stack operations and supports finding the stack's maximum element.

Implement the `MaxStack` class:

- `MaxStack()` Initializes the stack object.
- `void push(int x)` Pushes element `x` onto the stack.
- `int pop()` Removes the element on top of the stack and returns it.
- `int top()` Gets the element on the top of the stack without removing it.
- `int peekMax()` Retrieves the maximum element in the stack without removing it.
- `int popMax()` Retrieves the maximum element in the stack and removes it. If there is more than one maximum element, only remove the **top-most** one.

 

**Example 1:**

```
Input
["MaxStack", "push", "push", "push", "top", "popMax", "top", "peekMax", "pop", "top"]
[[], [5], [1], [5], [], [], [], [], [], []]
Output
[null, null, null, null, 5, 5, 1, 5, 1, 5]

Explanation
MaxStack stk = new MaxStack();
stk.push(5);   // [5] the top of the stack and the maximum number is 5.
stk.push(1);   // [5, 1] the top of the stack is 1, but the maximum is 5.
stk.push(5);   // [5, 1, 5] the top of the stack is 5, which is also the maximum, because it is the top most one.
stk.top();     // return 5, [5, 1, 5] the stack did not change.
stk.popMax();  // return 5, [5, 1] the stack is changed now, and the top is different from the max.
stk.top();     // return 1, [5, 1] the stack did not change.
stk.peekMax(); // return 5, [5, 1] the stack did not change.
stk.pop();     // return 1, [5] the top of the stack and the max element is now 5.
stk.top();     // return 5, [5] the stack did not change.
```

 

**Constraints:**

- `-107 <= x <= 107`
- At most `104` calls will be made to `push`, `pop`, `top`, `peekMax`, and `popMax`.
- There will be **at least one element** in the stack when `pop`, `top`, `peekMax`, or `popMax` is called.

 

**Follow up:** Could you come up with a solution that supports `O(1)` for each `top` call and `O(logn)` for each other call? 

思路：

- 对于pyhton要做到上述的事情是有一定困难的
- 一个普通的栈可以支持前三种操作 `push(x)`，`pop()` 和 `top()`，所以我们需要考虑的仅为后两种操作 `peekMax()` 和 `popMax()`。
- ![image-20220504211727323](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504211727323.png)

代码：

![image-20220504213658533](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504213658533.png)

#### [155. Min Stack](https://leetcode-cn.com/problems/min-stack/)

难度简单1280

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

 

**Example 1:**

```
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
```

 

**Constraints:**

- `-231 <= val <= 231 - 1`
- Methods `pop`, `top` and `getMin` operations will always be called on **non-empty** stacks.
- At most `3 * 104` calls will be made to `push`, `pop`, `top`, and `getMin`.

#### [828. 统计子串中的唯一字符](https://leetcode-cn.com/problems/count-unique-characters-of-all-substrings-of-a-given-string/)

难度困难109

我们定义了一个函数 `countUniqueChars(s)` 来统计字符串 `s` 中的唯一字符，并返回唯一字符的个数。

例如：`s = "LEETCODE"` ，则其中 `"L"`, `"T"`,`"C"`,`"O"`,`"D"` 都是唯一字符，因为它们只出现一次，所以 `countUniqueChars(s) = 5` 。

本题将会给你一个字符串 `s` ，我们需要返回 `countUniqueChars(t)` 的总和，其中 `t` 是 `s` 的子字符串。注意，某些子字符串可能是重复的，但你统计时也必须算上这些重复的子字符串（也就是说，你必须统计 `s` 的所有子字符串中的唯一字符）。

由于答案可能非常大，请将结果 **mod 10 ^ 9 + 7** 后再返回。

 

**示例 1：**

```
输入: s = "ABC"
输出: 10
解释: 所有可能的子串为："A","B","C","AB","BC" 和 "ABC"。
     其中，每一个子串都由独特字符构成。
     所以其长度总和为：1 + 1 + 1 + 2 + 2 + 3 = 10
```

**示例 2：**

```
输入: s = "ABA"
输出: 8
解释: 除了 countUniqueChars("ABA") = 1 之外，其余与示例 1 相同。
```

**示例 3：**

```
输入：s = "LEETCODE"
输出：92
```

 

**提示：**

- `0 <= s.length <= 10^5`
- `s` 只包含大写英文字符



#### [71. 简化路径](https://leetcode-cn.com/problems/simplify-path/)

难度中等475收藏分享切换为英文接收动态反馈

给你一个字符串 `path` ，表示指向某一文件或目录的 Unix 风格 **绝对路径** （以 `'/'` 开头），请你将其转化为更加简洁的规范路径。

在 Unix 风格的文件系统中，一个点（`.`）表示当前目录本身；此外，两个点 （`..`） 表示将目录切换到上一级（指向父目录）；两者都可以是复杂相对路径的组成部分。任意多个连续的斜杠（即，`'//'`）都被视为单个斜杠 `'/'` 。 对于此问题，任何其他格式的点（例如，`'...'`）均被视为文件/目录名称。

请注意，返回的 **规范路径** 必须遵循下述格式：

- 始终以斜杠 `'/'` 开头。
- 两个目录名之间必须只有一个斜杠 `'/'` 。
- 最后一个目录名（如果存在）**不能** 以 `'/'` 结尾。
- 此外，路径仅包含从根目录到目标文件或目录的路径上的目录（即，不含 `'.'` 或 `'..'`）。

返回简化后得到的 **规范路径** 。

 

**示例 1：**

```
输入：path = "/home/"
输出："/home"
解释：注意，最后一个目录名后面没有斜杠。 
```

**示例 2：**

```
输入：path = "/../"
输出："/"
解释：从根目录向上一级是不可行的，因为根目录是你可以到达的最高级。
```

**示例 3：**

```
输入：path = "/home//foo/"
输出："/home/foo"
解释：在规范路径中，多个连续斜杠需要用一个斜杠替换。
```

**示例 4：**

```
输入：path = "/a/./b/../../c/"
输出："/c"
```

 

**提示：**

- `1 <= path.length <= 3000`
- `path` 由英文字母，数字，`'.'`，`'/'` 或 `'_'` 组成。
- `path` 是一个有效的 Unix 风格绝对路径。

思路：

- 使用stack，在python中是列表
- 注意 `/a/b/c/..`是/a/b
- **Algorithm**
  1. Initialize a stack, `S` that we will be using for our implementation.
  2. **Split the input string using `/` as the delimiter.** 
     - This step is really important because no matter what, the given input is a `valid` path and we simply have to shorten it. So, that means that whatever we have between two `/` characters is either a directory name or a special character and we have to process them accordingly.
  3. Once we are done splitting the input path, we will process one component at a time.
  4. **If the current component is a `.` or an empty string,** **we will do nothing and simply continue.**
     - Well if you think about it, the split string array for the string **`/a//b` would be `[a,,b]`.** yes, that's an empty string in between `a` and `b`. Again, from the perspective of the overall path, it doesn't mean anything.
  5. **If we encounter a double-dot `..`**, we have to do some processing. This simply means go one level up in the current directory path. **So, we will pop an entry from our stack if it's not empty.**
  6. Finally, if the component we are processing right now is not one of the special characters, then we will simply add it to our stack because it's a legitimate directory name.
  7. Once we are done processing all the components, we simply have to connect all the directory names in our stack together using `/` as the delimiter and we will have our shortest path that leads us to the same directory as the one provided as an input.

代码：

![image-20220504124511610](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504124511610.png)

![image-20220504124535699](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504124535699.png)

#### [224. 基本计算器](https://leetcode-cn.com/problems/basic-calculator/)

难度困难750收藏分享切换为英文接收动态反馈

给你一个字符串表达式 `s` ，请你实现一个基本计算器来计算并返回它的值。

注意:不允许使用任何将字符串作为数学表达式计算的内置函数，比如 `eval()` 。

 

**示例 1：**

```
输入：s = "1 + 1"
输出：2
```

**示例 2：**

```
输入：s = " 2-1 + 2 "
输出：3
```

**示例 3：**

```
输入：s = "(1+(4+5+2)-3)+(6+8)"
输出：23
```

 

**提示：**

- `1 <= s.length <= 3 * 105`
- `s` 由数字、`'+'`、`'-'`、`'('`、`')'`、和 `' '` 组成
- `s` 表示一个有效的表达式
- '+' 不能用作一元运算(例如， "+1" 和 `"+(2 + 3)"` 无效)
- '-' 可以用作一元运算(即 "-1" 和 `"-(2 + 3)"` 是有效的)
- 输入中不存在两个连续的操作符
- 每个数字和运行的计算将适合于一个有符号的 32位 整数



思路：

- 好像处理括号匹配的问题常常会用到栈或者队列，感觉有点类似波兰表达式那道题，之后再看看

- 如果我们只是单纯把他插入stack再pop会有问题

  - ![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/Basic_Calculator_1.png)

- 我们应该先取反，再把它push到stack：

  - ![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/Basic_Calculator_2.png)

- Algorithm

  - When we encounter an opening parenthesis `(`, **this means an expression just ended.**（因为刚刚反转了） Recall we have reversed the expression. So an opening bracket would signify the end of the an expression. This calls for evaluation of the expression by popping operands and operators off the stack till we pop corresponding closing parenthesis. The final result of the expression is pushed back onto the stack.

- 上面这么做是由于“-”的处理，但是我们可以把“-”和数字绑在一起，用加号连接

  - ![image-20220504180657617](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504180657617.png)

- 例如，对于字符串1+2+(3-(4+5))：

  ![image-20220504181414306](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504181414306.png)

- **Algorithm**

  1. Iterate the expression string one character at a time. Since we are reading the expression character by character, we need to be careful when we are reading digits and non-digits.
  2. The operands could be formed by multiple characters. A string "123" would mean a numeric 123, which could be formed as: `123` >> `120 + 3` >> `100 + 20 + 3`. Thus, if the character read is a digit we need to form the operand by multiplying `10` to the previously formed continuing operand and adding the digit to it.
  3. Whenever we encounter an operator such as `+` or `-` we first evaluate the expression to the left and then save this `sign` for the next evaluation.![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/Basic_Calculator_4.png)
     - ![image-20220504183151611](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504183151611.png)![image-20220504183200857](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504183200857.png)
     - ![image-20220504183213770](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504183213770.png)![image-20220504183220697](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504183220697.png)
     - ![image-20220504183233783](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504183233783.png)![image-20220504183242772](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504183242772.png)
     - 
  4. If the character is an opening parenthesis `(`, we just push the result calculated so far and the `sign` on to the stack (the sign and the magnitude) and start a fresh as if we are calculating a new expression.
     - ![image-20220504183333940](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504183333940.png)
  5. If the character is a closing parenthesis `)`, we first calculate the expression to the left. The result from this would be the result of the expression within the set of parenthesis that just concluded. This result is then multiplied with the sign, if there is any on top of the stack. Remember we saved the `sign` on top of the stack when we had encountered an open parenthesis? This sign is associated with the parenthesis that started then, thus when the expression ends or concludes, we pop the `sign` and multiply it with result of the expression. It is then just added to the next element on top of the stack.
     - 如果字符是闭合括号），则首先计算左侧的表达式。从此的结果将是刚刚结束的括号内表达式的结果。然后，如果堆栈顶部有任何符号，则此结果将乘以标志。还记得当我们遇到开放括号时，我们将标志保存在堆栈顶部吗？该符号与当时开始的括号相关联，因此，当表达式结束或结论时，我们会弹出符号并乘以表达式的结果。然后仅将其添加到堆栈顶部的下一个元素中。
     - 注意 ( 时，会把 ( 前面的sign和result放进去
     - ![image-20220504183603911](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504183603911.png)

- 对于这个例子，在运行第一个右括号前，stack的样子：

  - ![image-20220504184324719](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504184324719.png)
  - 可以看到第一个左括号前是负号，所以是6，-1；第二个左括号前是负号，所以是8，-1，然后现在的sign还是存着9前面的负号，当前的result是负号前的7，operand是9

- 执行完第一个右括号：

  - ![image-20220504184607475](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504184607475.png)
  - 先是算出来里面的是-2：result += sign * operand
  - 再是pop出来8和-1
  - 对于-1是乘法，对于8是加法，所以现在result是10
  - 后面也一样，我们可以看到result就够了，operand就是0
  - 但是为什么result后面还要加一段呢？
  - 因为可能会有1+5这种情况，result只会存一个1，5存在operand里面，这就是安全没有调用stack的情况，就是没有处理括号的情况
  - ![image-20220504185404065](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504185404065.png)
  - 所以需要+sign*operand

代码：

![image-20220504182133271](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504182133271.png)



#### [227. 基本计算器 II](https://leetcode-cn.com/problems/basic-calculator-ii/)

难度中等553收藏分享切换为英文接收动态反馈

给你一个字符串表达式 `s` ，请你实现一个基本计算器来计算并返回它的值。

整数除法仅保留整数部分。

你可以假设给定的表达式总是有效的。所有中间结果将在 `[-231, 231 - 1]` 的范围内。

**注意：**不允许使用任何将字符串作为数学表达式计算的内置函数，比如 `eval()` 。

 

**示例 1：**

```
输入：s = "3+2*2"
输出：7
```

**示例 2：**

```
输入：s = " 3/2 "
输出：1
```

**示例 3：**

```
输入：s = " 3+5 / 2 "
输出：5
```

 

**提示：**

- `1 <= s.length <= 3 * 105`
- `s` 由整数和算符 `('+', '-', '*', '/')` 组成，中间由一些空格隔开
- `s` 表示一个 **有效表达式**
- 表达式中的所有整数都是非负整数，且在范围 `[0, 231 - 1]` 内
- 题目数据保证答案是一个 **32-bit 整数**

思路：

- Meta好像一直对这道题情有独钟
- 这道题不用进行括号判断
- 由于乘除优先于加减计算，因此不妨考虑先进行所有乘除运算，并将这些乘除运算后的整数值放回原表达式的相应位置，则随后整个表达式的值，就等于一系列整数加减后的值。
- 基于此，我们可以用一个栈，保存这些（进行乘除运算后的）整数的值。对于加减号后的数字，将其直接压入栈中；对于乘除号后的数字，可以直接与栈顶元素计算，并替换栈顶元素为计算后的结果。
- 一开始想和上一题一样直接用i，不用index，但是最后一位还有问题

![image-20220504193549198](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504193549198.png)

#### [65. 有效数字](https://leetcode-cn.com/problems/valid-number/)

难度困难310

**有效数字**（按顺序）可以分成以下几个部分：

1. 一个 **小数** 或者 **整数**
2. （可选）一个 `'e'` 或 `'E'` ，后面跟着一个 **整数**

**小数**（按顺序）可以分成以下几个部分：

1. （可选）一个符号字符（`'+'` 或 `'-'`）
2. 下述格式之一：
   1. 至少一位数字，后面跟着一个点 `'.'`
   2. 至少一位数字，后面跟着一个点 `'.'` ，后面再跟着至少一位数字
   3. 一个点 `'.'` ，后面跟着至少一位数字

**整数**（按顺序）可以分成以下几个部分：

1. （可选）一个符号字符（`'+'` 或 `'-'`）
2. 至少一位数字

部分有效数字列举如下：`["2", "0089", "-0.1", "+3.14", "4.", "-.9", "2e10", "-90E3", "3e+7", "+6e-1", "53.5e93", "-123.456e789"]`

部分无效数字列举如下：`["abc", "1a", "1e", "e3", "99e2.5", "--6", "-+3", "95a54e53"]`

给你一个字符串 `s` ，如果 `s` 是一个 **有效数字** ，请返回 `true` 。

 

**示例 1：**

```
输入：s = "0"
输出：true
```

**示例 2：**

```
输入：s = "e"
输出：false
```

**示例 3：**

```
输入：s = "."
输出：false
```

 

**提示：**

- `1 <= s.length <= 20`
- `s` 仅含英文字母（大写和小写），数字（`0-9`），加号 `'+'` ，减号 `'-'` ，或者点 `'.'` 。

思路：

- this is not your typical LeetCode problem, but a problem that is highly representative of a "real world" problem - a seemingly simple task that is frustratingly full of edge cases.
- **Interview Tip:** Asked a question like this in an interview? Be sure to communicate thoroughly with your interviewer to make sure you're covering all cases.
- 如果到目前为止它可以认为是数字，就让seen_digit为True，如果碰到e，就要设置他为false
  - At the end, return `seenDigit`. This is one reason why we have to reset `seenDigit` after seeing an exponent - otherwise an input like `"21e"` would be incorrectly judged as valid.
  - 但也需要注意，dot不需要前面有digit，也不需要后面有，比如4.也是ok的

代码：

![image-20220504120110179](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220504120110179.png)

- 时间复杂度是O(N)
- 空间复杂度是O(1)