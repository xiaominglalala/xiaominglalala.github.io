---
layout:     post
title:      Two Pointers (Finished)
subtitle:   
date:       2022-04-13
author:     Ethan
header-img: img/city_10.jpg
catalog: true
tags:
    - Leetcode
    - Two Pointers
---
## 双指针

#### [27. 移除元素](https://leetcode-cn.com/problems/remove-element/)

难度简单1132

给你一个数组 `nums` 和一个值 `val`，你需要 **[原地](https://baike.baidu.com/item/原地算法)** 移除所有数值等于 `val` 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 `O(1)` 额外空间并 **[原地 ](https://baike.baidu.com/item/原地算法)修改输入数组**。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

 

**说明:**

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以**「引用」**方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

```
// nums 是以“引用”方式传递的。也就是说，不对实参作任何拷贝
int len = removeElement(nums, val);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

**示例 1：**

```
输入：nums = [3,2,2,3], val = 3
输出：2, nums = [2,2]
解释：函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。你不需要考虑数组中超出新长度后面的元素。例如，函数返回的新长度为 2 ，而 nums = [2,2,3,3] 或 nums = [2,2,0,0]，也会被视作正确答案。
```

**示例 2：**

```
输入：nums = [0,1,2,2,3,0,4,2], val = 2
输出：5, nums = [0,1,4,0,3]
解释：函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。注意这五个元素可为任意顺序。你不需要考虑数组中超出新长度后面的元素。
```

思路：<img src="C:\Users\Ethan\AppData\Roaming\Typora\typora-user-images\image-20211230223738928.png" alt="image-20211230223738928" style="zoom: 10%;" />

- 一开始没遇到val，fast和slow在一起，所以交换没有关系，
- 当遇到val，fast继续前进，直到遇到不是val或者走出去。
- 再和slow交换

代码：

![image-20220425113615530](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220425113615530.png)

为什么是slow不是slow + 1

#### [26. 删除有序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

难度简单2585

给你一个 **升序排列** 的数组 `nums` ，请你**[ 原地](http://baike.baidu.com/item/原地算法)** 删除重复出现的元素，使每个元素 **只出现一次** ，返回删除后数组的新长度。元素的 **相对顺序** 应该保持 **一致** 。

由于在某些语言中不能改变数组的长度，所以必须将结果放在数组nums的第一部分。更规范地说，如果在删除重复项之后有 `k` 个元素，那么 `nums` 的前 `k` 个元素应该保存最终结果。

将最终结果插入 `nums` 的前 `k` 个位置后返回 `k` 。

不要使用额外的空间，你必须在 **[原地 ](https://baike.baidu.com/item/原地算法)修改输入数组** 并在使用 O(1) 额外空间的条件下完成。

**判题标准:**

系统会用下面的代码来测试你的题解:

```
int[] nums = [...]; // 输入数组
int[] expectedNums = [...]; // 长度正确的期望答案

int k = removeDuplicates(nums); // 调用

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
```

如果所有断言都通过，那么您的题解将被 **通过**。

 

**示例 1：**

```
输入：nums = [1,1,2]
输出：2, nums = [1,2,_]
解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。
```

**示例 2：**

```
输入：nums = [0,0,1,1,1,2,2,3,3,4]
输出：5, nums = [0,1,2,3,4]
解释：函数应该返回新的长度 5 ， 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4 。不需要考虑数组中超出新长度后面的元素。
```

 

**提示：**

- `0 <= nums.length <= 3 * 104`
- `-104 <= nums[i] <= 104`
- `nums` 已按 **升序** 排列

![image-20220425120812489](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220425120812489.png)

#### [80. 删除有序数组中的重复项 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii/)

难度中等672

给你一个有序数组 `nums` ，请你**[ 原地](http://baike.baidu.com/item/原地算法)** 删除重复出现的元素，使每个元素 **最多出现两次** ，返回删除后数组的新长度。

不要使用额外的数组空间，你必须在 **[原地 ](https://baike.baidu.com/item/原地算法)修改输入数组** 并在使用 O(1) 额外空间的条件下完成。

 

**说明：**

为什么返回数值是整数，但输出的答案是数组呢？

请注意，输入数组是以**「引用」**方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

```
// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

 

**示例 1：**

```
输入：nums = [1,1,1,2,2,3]
输出：5, nums = [1,1,2,2,3]
解释：函数应返回新长度 length = 5, 并且原数组的前五个元素被修改为 1, 1, 2, 2, 3 。 不需要考虑数组中超出新长度后面的元素。
```

**示例 2：**

```
输入：nums = [0,0,1,1,1,1,2,3,3]
输出：7, nums = [0,0,1,1,2,3,3]
解释：函数应返回新长度 length = 7, 并且原数组的前五个元素被修改为 0, 0, 1, 1, 2, 3, 3 。 不需要考虑数组中超出新长度后面的元素。
```

 

**提示：**

- `1 <= nums.length <= 3 * 104`
- `-104 <= nums[i] <= 104`
- `nums` 已按升序排列

思路：

![image-20220426103224730](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220426103224730.png)

时间复杂度O(N),空间复杂度O(1)



#### [283. 移动零](https://leetcode-cn.com/problems/move-zeroes/)

难度简单1548收藏分享切换为英文接收动态反馈

给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。

**请注意** ，必须在不复制数组的情况下原地对数组进行操作。

 

**示例 1:**

```
输入: nums = [0,1,0,3,12]
输出: [1,3,12,0,0]
```

**示例 2:**

```
输入: nums = [0]
输出: [0]
```

 

**提示**:

- `1 <= nums.length <= 104`
- `-231 <= nums[i] <= 231 - 1`

 

**进阶：**你能尽量减少完成的操作次数吗？

思路：

- 使用双指针，slow在0，fast在1
- fast在迭代的过程中，
  - 如果fast指向的位置不是0，而slow的是0，就把fast和slow调换
  - 如果slow不是0，slow加1
- 注意第一个if里面也要给slow+1！

![image-20220426105310541](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220426105310541.png)

#### [844. 比较含退格的字符串](https://leetcode-cn.com/problems/backspace-string-compare/)

难度简单408收藏分享切换为英文接收动态反馈

给定 `s` 和 `t` 两个字符串，当它们分别被输入到空白的文本编辑器后，如果两者相等，返回 `true` 。`#` 代表退格字符。

**注意：**如果对空文本输入退格字符，文本继续为空。

 

**示例 1：**

```
输入：s = "ab#c", t = "ad#c"
输出：true
解释：s 和 t 都会变成 "ac"。
```

**示例 2：**

```
输入：s = "ab##", t = "c#d#"
输出：true
解释：s 和 t 都会变成 ""。
```

**示例 3：**

```
输入：s = "a#c", t = "b"
输出：false
解释：s 会变成 "c"，但 t 仍然是 "b"。
```

 

**提示：**

- `1 <= s.length, t.length <= 200`
- `s` 和 `t` 只含有小写字母以及字符 `'#'`

 

**进阶：**

- 你可以用 `O(n)` 的时间复杂度和 `O(1)` 的空间复杂度解决该问题吗？

思路：

- string 不能这样赋值 ：string[slow] = string[fast]
- 所以先保留每个字母到新的list，再合并
- 注意#要pop出去一个

代码：

时间复杂度：O(N+M)，其中 N 和 M 分别为字符串 S 和 T 的长度。我们需要遍历两字符串各一次。

空间复杂度：O(N+M)，其中 N 和 M 分别为字符串 S和 T 的长度。主要为还原出的字符串的开销。



![image-20220416184358875](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220416184358875.png)



如何使用O(1)的空间？

- 一个字符是否会被删掉，只取决于该字符后面的退格符，而与该字符前面的退格符无关。因此当我们逆序地遍历字符串，就可以立即确定当前字符是否会被删掉
- 首先是倒序遍历，然后定义skip来记录需要多少个跳过
- 每次只比一位！
- 假设我们有“ab#c”和“ad#c”
  现在，我们从末尾开始遍历
  - i = 3 和 j = 3：
    - 我们看到 S[i] 和 T[j] 是**有效字符**。因此，我们只是比较它们，然后分别减小 i 和 j 的值。现在我们要比较“ab#”和ad#”
  - i = 2 和 j = 2：
    - 我们看到 S[i] 不是一个**有效的字符**。因此，我们必须跳过可能遇到的下一个**有效字符。**在这种情况下，我们跳过“b”。现在必须与下一个未被跳过的**有效字符进行比较，即“a”。**类似地，在 T[j] 的情况下，下一个**有效字符**是“a”。我们比较两者，它们匹配。

![image-20220426113814283](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220426113814283.png)

注意第34行，# eg. S = "a#", T = "a"

#### [977. 有序数组的平方](https://leetcode-cn.com/problems/squares-of-a-sorted-array/)

难度简单498收藏分享切换为英文接收动态反馈

给你一个按 **非递减顺序** 排序的整数数组 `nums`，返回 **每个数字的平方** 组成的新数组，要求也按 **非递减顺序** 排序。



 

**示例 1：**

```
输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]
解释：平方后，数组变为 [16,1,0,9,100]
排序后，数组变为 [0,1,9,16,100]
```

**示例 2：**

```
输入：nums = [-7,-3,2,3,11]
输出：[4,9,9,49,121]
```

 

**提示：**

- `1 <= nums.length <= 104`
- `-104 <= nums[i] <= 104`
- `nums` 已按 **非递减顺序** 排序

 

**进阶：**

- 请你设计时间复杂度为 `O(n)` 的算法解决本问题



思路：

假如使用暴力法，对于数组平方后再排序，时间复杂度是O(nlgn), 空间复杂度是O(lgn)

代码：

![image-20220416175921117](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220416175921117.png)

- 另一种方法是我们可以使用两个指针分别指向位置 0 和 n-1，每次比较两个指针对应的数，选择较大的那个逆序放入答案并移动指针。这种方法无需处理某一指针移动至边界的情况，
  - 时间复杂度是O(n), 空间复杂度是O(N).

![image-20220416182830811](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220416182830811.png)

#### [344. 反转字符串](https://leetcode-cn.com/problems/reverse-string/)

难度简单504

编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 `s` 的形式给出。

不要给另外的数组分配额外的空间，你必须**[原地](https://baike.baidu.com/item/原地算法)修改输入数组**、使用 O(1) 的额外空间解决这一问题。

 

**示例 1：**

```
输入：s = ["h","e","l","l","o"]
输出：["o","l","l","e","h"]
```

**示例 2：**

```
输入：s = ["H","a","n","n","a","h"]
输出：["h","a","n","n","a","H"]
```

代码：

![image-20220426105953207](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220426105953207.png)

时间复杂度O(n), 空间复杂度O(1)

#### [剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

难度简单193

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

 

**示例 1：**

```
输入：s = "We are happy."
输出："We%20are%20happy."
```

思路：

移除类和替换类双指针还蛮适合的

代码：

![image-20220416193006373](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220416193006373.png)

- **时间复杂度 O(N)：** 遍历使用 O(N)，每轮添加（修改）字符操作使用)*O*(1) ；
- **空间复杂度 O(N)** 

**其实很多数组填充类的问题，都可以先预先给数组扩容带填充后的大小，然后在从后向前进行操作。**

这么做有两个好处：

1. 不用申请新数组。
2. 从后向前填充元素，避免了从前先后填充元素要来的 每次添加元素都要将添加元素之后的所有元素向后移动。

如果希望空间复杂度是(1), 那么就原地扩展s。先计算出需要几个空格，再把s扩充到那么长，再双指针修改

![image-20220416203948930](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220416203948930.png)

#### [151. Reverse Words in a String](https://leetcode-cn.com/problems/reverse-words-in-a-string/)

难度中等511

Given an input string `s`, reverse the order of the **words**.

A **word** is defined as a sequence of non-space characters. The **words** in `s` will be separated by at least one space.

Return *a string of the words in reverse order concatenated by a single space.*

**Note** that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

 

**Example 1:**

```
Input: s = "the sky is blue"
Output: "blue is sky the"
```

**Example 2:**

```
Input: s = "  head += 1 world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```

**Example 3:**

```
Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

 

**Constraints:**

- `1 <= s.length <= 104`
- `s` contains English letters (upper-case and lower-case), digits, and spaces `' '`.
- There is **at least one** word in `s`.

 

**Follow-up:** If the string data type is mutable in your language, can you solve it **in-place** with `O(1)` extra space?



思路：

- 使用split库函数，分隔单词，然后定义一个新的string字符串，最后再把单词倒序相加，那么这道题题目就是一道水题了，失去了它的意义

![image-20220416202726483](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220416202726483.png)

- 本题的难点在于：**不要使用辅助空间，空间复杂度要求为O(1)**  但只有C++可以做到，需要使用指针。python还是O(n)，因为python的字符串str是不可变的，如果要用list，就要多余的空间
- 不能使用辅助空间之后，那么只能在原字符串上下功夫了
- 所以解题思路如下：
  - 移除多余空格
  - 将整个字符串反转
  - 将每个单词反转
- 举个例子，源字符串为："the sky is blue "
  - 移除多余空格 : "the sky is blue"
  - 字符串反转："eulb si yks eht"
  - 单词反转："blue is sky the"
- 使用双指针法来去移除空格，最后resize（重新设置）一下字符串的大小，就可以做到O(n)的时间复杂度。

代码：

![image-20220426150017842](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220426150017842.png)



#### [206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

难度简单2172

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

```
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

```
输入：head = [1,2]
输出：[2,1]
```

**示例 3：**

```
输入：head = []
输出：[]
```

思路：

- 如果再定义一个新的链表，实现链表元素的反转，其实这是对内存空间的浪费。

  其实只需要改变链表的next指针的指向，直接将链表反转 

- <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/008eGmZEly1gnrf1oboupg30gy0c44qp.gif" alt="img" style="zoom:50%;" />

- 

代码：

Iteration：

![image-20220426151112265](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220426151112265.png)

Recursion：

![image-20220426151357493](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220426151357493.png)

#### [19. Remove Nth Node From End of List](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

难度中等1958

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/remove_ex1.jpg)

```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

**Example 2:**

```
Input: head = [1], n = 1
Output: []
```

**Example 3:**

```
Input: head = [1,2], n = 1
Output: [1]
```

 

**Constraints:**

- The number of nodes in the list is `sz`.
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

 

**Follow up:** Could you do this in one pass?



思路：

- 双指针的经典应用，如果要删除倒数第n个节点，让fast移动n步，然后让fast和slow同时移动，直到fast指向链表末尾。删掉slow.next就可以了。
- 由于可能会涉及要删除实际的头节点，所以最好设置虚拟头节点

代码：

![image-20220426192236050](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220426192236050.png)

#### [15. 三数之和](https://leetcode-cn.com/problems/3sum/) & [剑指 Offer II 007. 数组中和为 0 的三个数](https://leetcode-cn.com/problems/1fGaJU/)

难度中等51

给定一个包含 `n` 个整数的数组 `nums`，判断 `nums` 中是否存在三个元素 `a` ，`b` ，`c` *，*使得 `a + b + c = 0` ？请找出所有和为 `0` 且 **不重复** 的三元组。

 

**示例 1：**

```
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
```

**示例 2：**

```
输入：nums = []
输出：[]
```

**示例 3：**

```
输入：nums = [0]
输出：[]
```

思路：

- 首先将数组排序，将索引i定在下标0的地方开始，同时索引left 定义在i+1的位置上，定义索引right 在数组结尾的位置上。
-  a = nums[i] b = nums[left] c = nums[right]
- 如果nums[i] + nums[left] + nums[right] > target 就说明 此时三数之和大了，因为数组是排序后了，所以right下标就应该向左移动，这样才能让三数之和小一些。
- 如果 nums[i] + nums[left] + nums[right] < target 说明 此时 三数之和小了，left 就向右移动，才能让三数之和大一些，直到left与right相遇为止。
- 注意对于要放入result的三元组，会要走到最后一个重复的，比如222333456，left取2，他就会让left取到最后一个2，然后再+=1，取到3，进行下次计算

代码：

![image-20220426223513805](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220426223513805.png)

#### 16. 3Sum Closest

Medium

5717245Add to ListShare

Given an integer array `nums` of length `n` and an integer `target`, find three integers in `nums` such that the sum is closest to `target`.

Return *the sum of the three integers*.

You may assume that each input would have exactly one solution.

 

**Example 1:**

```
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

**Example 2:**

```
Input: nums = [0,0,0], target = 1
Output: 0
```

 

**Constraints:**

- `3 <= nums.length <= 1000`
- `-1000 <= nums[i] <= 1000`
- `-104 <= target <= 104`

思路：

- 存储当前的最近，根据数值范围现先给一个很大的result

代码：

![image-20220426235127492](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220426235127492.png)

#### [18. 四数之和](https://leetcode-cn.com/problems/4sum/)

难度中等1057

给你一个由 `n` 个整数组成的数组 `nums` ，和一个目标值 `target` 。请你找出并返回满足下述全部条件且**不重复**的四元组 `[nums[a], nums[b], nums[c], nums[d]]` （若两个四元组元素一一对应，则认为两个四元组重复）：

- `0 <= a, b, c, d < n`
- `a`、`b`、`c` 和 `d` **互不相同**
- `nums[a] + nums[b] + nums[c] + nums[d] == target`

你可以按 **任意顺序** 返回答案 。

 

**示例 1：**

```
输入：nums = [1,0,-1,0,-2,2], target = 0
输出：[[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
```

**示例 2：**

```
输入：nums = [2,2,2,2,2], target = 8
输出：[[2,2,2,2]]
```

思路：

- 和[15.三数之和 (opens new window)](https://programmercarl.com/0015.三数之和.html)是一个思路，都是使用双指针法, 基本解法就是在[15.三数之和 (opens new window)](https://programmercarl.com/0015.三数之和.html)的基础上再套一层for循环。
- 对于[15.三数之和 (opens new window)](https://programmercarl.com/0015.三数之和.html)双指针法就是将原本暴力$O(n^3)$的解法，降为$O(n^2)$的解法，四数之和的双指针解法就是将原本暴力$O(n^4)$的解法，降为$O(n^3)$的解法。
- 三数之和的双指针是用for循环确定nums[i], 然后使用双指针找到nums[left], nums[right]
- 四数之和是两层for循环确定nums[i], nums[j],然后最里面的循环使用双指针找到nums[left], nums[right]

代码：

注意可能存在重负的数字，所以要去重，这也就是sort的意义，16题不用因为它不在乎有哪些数字组合的，只要结果的数字，但是15题和这题一样要注意这一点。

还有就是就是取一样的

![image-20220430095513275](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220430095513275.png)

注意就是第六行和第九行的两个判断，i和j都是在取第二个值才开始判断是否重复，而且是往后看，这样就保证至少第一次取没关系

而且要注意17和19行在找left和right的重复时，要保证left<right

![image-20220430095821592](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220430095821592.png)



#### [167. 两数之和 II - 输入有序数组](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)

难度中等761收藏分享切换为英文接收动态反馈

给你一个下标从 **1** 开始的整数数组 `numbers` ，该数组已按 **非递减顺序排列** ，请你从数组中找出满足相加之和等于目标数 `target` 的两个数。如果设这两个数分别是 `numbers[index1]` 和 `numbers[index2]` ，则 `1 <= index1 < index2 <= numbers.length` 。

以长度为 2 的整数数组 `[index1, index2]` 的形式返回这两个整数的下标 `index1` 和 `index2`。

你可以假设每个输入 **只对应唯一的答案** ，而且你 **不可以** 重复使用相同的元素。

你所设计的解决方案必须只使用常量级的额外空间。

**示例 1：**

```
输入：numbers = [2,7,11,15], target = 9
输出：[1,2]
解释：2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。返回 [1, 2] 。
```

**示例 2：**

```
输入：numbers = [2,3,4], target = 6
输出：[1,3]
解释：2 与 4 之和等于目标数 6 。因此 index1 = 1, index2 = 3 。返回 [1, 3] 。
```

**示例 3：**

```
输入：numbers = [-1,0], target = -1
输出：[1,2]
解释：-1 与 0 之和等于目标数 -1 。因此 index1 = 1, index2 = 2 。返回 [1, 2] 。
```

 

**提示：**

- `2 <= numbers.length <= 3 * 104`
- `-1000 <= numbers[i] <= 1000`
- `numbers` 按 **非递减顺序** 排列
- `-1000 <= target <= 1000`
- **仅存在一个有效答案**

思路：

因为只有一个答案，所以不用太担心重复

此外，不是返回python索引，从0开始。而是从1开始，这个细节面试一定要注意

![image-20220430100944576](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220430100944576.png)

#### [259. 较小的三数之和](https://leetcode-cn.com/problems/3sum-smaller/)

难度中等108

给定一个长度为 `n` 的整数数组和一个目标值 `target` ，寻找能够使条件 `nums[i] + nums[j] + nums[k] < target` 成立的三元组 `i, j, k` 个数（`0 <= i < j < k < n`）。

 

**示例 1：**

```
输入: nums = [-2,0,1,3], target = 2
输出: 2 
解释: 因为一共有两个三元组满足累加和小于 2:
     [-2,0,1]
     [-2,0,3]
```

**示例 2：**

```
输入: nums = [], target = 0
输出: 0 
```

**示例 3：**

```
输入: nums = [0], target = 0
输出: 0 
```

 

**提示:**

- `n == nums.length`
- `0 <= n <= 3500`
- `-100 <= nums[i] <= 100`
- `-100 <= target <= 100`

![image-20220430102952035](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220430102952035.png)



#### [31. 下一个排列](https://leetcode-cn.com/problems/next-permutation/)

难度中等1647

整数数组的一个 **排列** 就是将其所有成员以序列或线性顺序排列。

- 例如，`arr = [1,2,3]` ，以下这些都可以视作 `arr` 的排列：`[1,2,3]`、`[1,3,2]`、`[3,1,2]`、`[2,3,1]` 。

整数数组的 **下一个排列** 是指其整数的下一个字典序更大的排列。更正式地，如果数组的所有排列根据其字典顺序从小到大排列在一个容器中，那么数组的 **下一个排列** 就是在这个有序容器中排在它后面的那个排列。如果不存在下一个更大的排列，那么这个数组必须重排为字典序最小的排列（即，其元素按升序排列）。

- 例如，`arr = [1,2,3]` 的下一个排列是 `[1,3,2]` 。
- 类似地，`arr = [2,3,1]` 的下一个排列是 `[3,1,2]` 。
- 而 `arr = [3,2,1]` 的下一个排列是 `[1,2,3]` ，因为 `[3,2,1]` 不存在一个字典序更大的排列。

给你一个整数数组 `nums` ，找出 `nums` 的下一个排列。

必须**[ 原地 ](https://baike.baidu.com/item/原地算法)**修改，只允许使用额外常数空间。

 

**示例 1：**

```
输入：nums = [1,2,3]
输出：[1,3,2]
```

**示例 2：**

```
输入：nums = [3,2,1]
输出：[1,2,3]
```

**示例 3：**

```
输入：nums = [1,1,5]
输出：[1,5,1]
```

思路：

In this approach, we find out every possible permutation of list formed by the elements of the given array and find out the permutation which is just larger than the given one. But this one will be a very naive approach, since it requires us to find out every possible permutation which will take really long time and the implementation is complex. Thus, this approach is not acceptable at all. Hence, we move on directly to the correct approach.

- Time complexity : O(n!). Total possible permutations is n!*n*!.
- Space complexity : O(n). Since an array will be used to store the permutations.

First, we observe that for any given sequence that is in decreasing order, no next larget permutation is possible. For example, [9,5,4,3,1]

We need to find the first pair of a[i] and a[i-1] from the right, which satisfy a[i] < a[i-1]

We want to create the permutation just larger than the current one. Therefore, we need to replace a[i-1] with the number just larger than itself on his right, like a[j]

![ Next Permutation ](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/31_nums_graph.png)

We swap a[i-1] and a[j], all numbers to the right of a[i-1]were already sorted in descending order. Furthermore, swapping a[i-1] and a[j] didn't change that order. Therefore, we simply need to reverse the numbers following a[i-1] to get the next smallest lexicographic permutation.

我们还希望下一个数增加的幅度尽可能的小，这样才满足“下一个排列与当前排列紧邻“的要求。为了满足这个要求，我们需要：
在尽可能靠右的低位进行交换，需要从后向前查找
将一个 尽可能小的「大数」 与前面的「小数」交换。比如 123465，下一个排列应该把 5 和 4 交换而不是把 6 和 4 交换
将「大数」换到前面后，需要将「大数」后面的所有数重置为升序，升序排列就是最小的排列。以 123465 为例：首先按照上一步，交换 5 和 4，得到 123564；然后需要将 5 之后的数重置为升序，得到 123546。显然 123546 比 123564 更小，123546 就是 123465 的下一个排列

算法过程：

从后向前查找第一个相邻升序的元素对 (i,j)，满足 A[i] < A[j]。此时 [j,end) 必然是降序
在 [j,end) 从后向前查找第一个满足 A[i] < A[k] 的 k。A[i]、A[k] 分别就是上文所说的「小数」、「大数」
将 A[i] 与 A[k] 交换
可以断定这时 [j,end) 必然是降序，逆置 [j,end)，使其升序
如果在步骤 1 找不到符合的相邻元素对，说明当前 [begin,end) 为一个降序顺序，则直接跳到步骤 4

<img src="https://pic.leetcode-cn.com/6e8c9822771be77c6f34cd3086153984eec386fb8376e09e36132ac36bb9cd6f-image.png" alt="image.png" style="zoom: 67%;" />

首先从后向前找到第一个相邻的升序元素，这里是5，7；注意，找到5，7说明7后面都是递减的

<img src="https://pic.leetcode-cn.com/d7acefea4f7d4e2f19fb5eaa269c448a3098eee53656926a0ab592c564dde150-image.png" alt="image.png" style="zoom:67%;" />

然后在7后面找到第一个比5大的，就是6

<img src="https://pic.leetcode-cn.com/061cf291c237e6f5bcd0554192f894cd0c3e361b4564aa542aabe96e644afbf1-image.png" alt="image.png" style="zoom:67%;" />

交换5，6

<img src="https://pic.leetcode-cn.com/eb1470fd9942da6d2ab4855d13dfadcb715b629b4ea9cba0edfe2d1298744186-image.png" alt="image.png" style="zoom:67%;" />

此时7后面依然是保持递减的关系，然后反转754变成457

<img src="https://pic.leetcode-cn.com/9d627a4ffda635bbf0c4fcdb7b1359c557db8e1c300ab54383a0bc89f6763c18-image.png" alt="image.png" style="zoom:67%;" />

<img src="https://pic.leetcode-cn.com/e56a66ed318d1761cd8c8f9d1521f82a30c71ecc84f551912b90d8fe254c8f3d-image.png" alt="image.png" style="zoom:67%;" />



代码：

注意如果已经是递减了，就反过来，从头来过。第一个。

![image-20220430114607330](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220430114607330.png)

#### [88. 合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)

难度简单1389

给你两个按 **非递减顺序** 排列的整数数组 `nums1` 和 `nums2`，另有两个整数 `m` 和 `n` ，分别表示 `nums1` 和 `nums2` 中的元素数目。

请你 **合并** `nums2` 到 `nums1` 中，使合并后的数组同样按 **非递减顺序** 排列。

**注意：**最终，合并后数组不应由函数返回，而是存储在数组 `nums1` 中。为了应对这种情况，`nums1` 的初始长度为 `m + n`，其中前 `m` 个元素表示应合并的元素，后 `n` 个元素为 `0` ，应忽略。`nums2` 的长度为 `n` 。

 

**示例 1：**

```
输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
输出：[1,2,2,3,5,6]
解释：需要合并 [1,2,3] 和 [2,5,6] 。
合并结果是 [1,2,2,3,5,6] ，其中斜体加粗标注的为 nums1 中的元素。
```

**示例 2：**

```
输入：nums1 = [1], m = 1, nums2 = [], n = 0
输出：[1]
解释：需要合并 [1] 和 [] 。
合并结果是 [1] 。
```

**示例 3：**

```
输入：nums1 = [0], m = 0, nums2 = [1], n = 1
输出：[1]
解释：需要合并的数组是 [] 和 [1] 。
合并结果是 [1] 。
注意，因为 m = 0 ，所以 nums1 中没有元素。nums1 中仅存的 0 仅仅是为了确保合并结果可以顺利存放到 nums1 中。
```

 

**提示：**

- `nums1.length == m + n`
- `nums2.length == n`
- `0 <= m, n <= 200`
- `1 <= m + n <= 200`
- `-109 <= nums1[i], nums2[j] <= 109`

 

**进阶：**你可以设计实现一个时间复杂度为 `O(m + n)` 的算法解决此问题吗？

思路：

- 双指针，为了避免覆盖，取nums1和nums2中的后面

代码：

![image-20220430161910560](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220430161910560.png)

#### [189. 轮转数组](https://leetcode-cn.com/problems/rotate-array/)

难度中等1446

给你一个数组，将数组中的元素向右轮转 `k` 个位置，其中 `k` 是非负数。

 

**示例 1:**

```
输入: nums = [1,2,3,4,5,6,7], k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右轮转 1 步: [7,1,2,3,4,5,6]
向右轮转 2 步: [6,7,1,2,3,4,5]
向右轮转 3 步: [5,6,7,1,2,3,4]
```

**示例 2:**

```
输入：nums = [-1,-100,3,99], k = 2
输出：[3,99,-1,-100]
解释: 
向右轮转 1 步: [99,-1,-100,3]
向右轮转 2 步: [3,99,-1,-100]
```

 

**提示：**

- `1 <= nums.length <= 105`
- `-231 <= nums[i] <= 231 - 1`
- `0 <= k <= 105`

 

**进阶：**

- 尽可能想出更多的解决方案，至少有 **三种** 不同的方法可以解决这个问题。
- 你可以使用空间复杂度为 `O(1)` 的 **原地** 算法解决这个问题吗

思路：

- 如果使用暴力法，就先求出k%n，以防止k是比n大很多很多
- 然后提取出最后一位，然后从头开始依次轮换
- 这样的轮换需要做k%n次

![image-20220501230519779](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220501230519779.png)



- 如果希望原地替换，使用O(1)的空间复杂度
- 外面使用变量temp来保存需要替换的item， 位置为0的会被放在x=(0+k)%len(nums)的位置， 令temp = nums[x], 此时交换temp和x[0]
- 不断循环直到再次来到0位置
- 使用count来计数，把count = len(nums)作为循环退出的判断条件。
- ![Rotate Array](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/189_Rotate_Array.png)
- 这是因为从头开始是不会遍历所有的点的，比如从1开始，只会是1，3，5.
- 此时需要break一下，break的条件是回到了1，然后让开始的点加1

![image-20220501234153712](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220501234153712.png)

reverse之后试试

![image-20220501231828155](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220501231828155.png)

#### [42. Trapping Rain Water](https://leetcode-cn.com/problems/trapping-rain-water/)

难度困难3336

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

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

 

**Constraints:**

- `n == height.length`
- `1 <= n <= 2 * 104`
- `0 <= height[i] <= 105`

<img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220502124555172.png" alt="image-20220502124555172" style="zoom: 80%;" />

- 对于下标i，如果它两边是封闭的，它的储水量为最矮的一边减去下标i的高度
- ![image-20220502134832115](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220502134832115.png)
- 注意是找到左右max中的最小，找左右max才是真正包裹它的，而最小才是它真正可以触及到的
- 这样是O(N^2)

如果已经知道每个位置的两边的最大高度，则可以在O(N)完成，使用动态规划来预处理最大高度

- leftmax[i]代表i节点及其左边的位置中，最高的高度

- rightmax[i]代表i节点及其右边的位置中，最高的高度

- 正向遍历height得到leftmax，反向遍历height得到rightmax
- <img src="https://raw.githubusercontent.com/xiaominglalala/pic/main/img/1.png" alt="fig1" style="zoom: 33%;" />
- ![image-20220502144019929](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220502144019929.png)

由于需要维护left_max和right_max两个数组，所有空间复杂度为O(n)

- 使用双指针，维护两个指针left = 0，right = len(n) - 1; 两个变量left_max, right_max

- 定理一：在某个位置`i`处，它能存的水，取决于它左右两边的最大值中较小的一个。

  定理二：当我们从左往右处理到left下标时，左边的最大值left_max对它而言是可信的，但right_max对它而言是不可信的。（见下图，由于中间状况未知，对于left下标而言，right_max未必就是它右边最大的值）

  定理三：当我们从右往左处理到right下标时，右边的最大值right_max对它而言是可信的，但left_max对它而言是不可信的。

- 对于位置`left`而言，它左边最大值一定是left_max，右边最大值“大于等于”right_max，这时候，如果`left_max<right_max`成立，那么它就知道自己能存多少水了。无论右边将来会不会出现更大的right_max，都不影响这个结果。 所以当`left_max<right_max`时，我们就希望去处理left下标，反之，我们希望去处理right下标

- ![image-20220502144941056](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220502144941056.png)

- ![image-20220502145610153](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220502145610153.png)

#### [11. Container With Most Water](https://leetcode-cn.com/problems/container-with-most-water/)

难度中等3397

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return *the maximum amount of water a container can store*.

**Notice** that you may not slant the container.

 

**Example 1:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/question_11.jpg)

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

**Example 2:**

```
Input: height = [1,1]
Output: 1
```

 

**Constraints:**

- `n == height.length`
- `2 <= n <= 105`
- `0 <= height[i] <= 104`

思路：

- 首先要意识到必须每一列一样高，否则全倒水就完事了
- 很容易的想法是min(nums[left] - nums[right]) * (len(right) - len(left))
- ![image-20220502151544434](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220502151544434.png)

#### [539. 最小时间差](https://leetcode-cn.com/problems/minimum-time-difference/) & [剑指 Offer II 035. 最小时间差](https://leetcode-cn.com/problems/569nqc/) 

难度中等193

给定一个 24 小时制（小时:分钟 **"HH:MM"**）的时间列表，找出列表中任意两个时间的最小时间差并以分钟数表示。

 

**示例 1：**

```
输入：timePoints = ["23:59","00:00"]
输出：1
```

**示例 2：**

```
输入：timePoints = ["00:00","23:59","00:00"]
输出：0
```

思路:

排序，排序后最小的要么是首尾，要么是中间

代码：

![image-20220502154716750](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220502154716750.png)

#### [165. 比较版本号](https://leetcode-cn.com/problems/compare-version-numbers/)

难度中等278

给你两个版本号 `version1` 和 `version2` ，请你比较它们。

版本号由一个或多个修订号组成，各修订号由一个 `'.'` 连接。每个修订号由 **多位数字** 组成，可能包含 **前导零** 。每个版本号至少包含一个字符。修订号从左到右编号，下标从 0 开始，最左边的修订号下标为 0 ，下一个修订号下标为 1 ，以此类推。例如，`2.5.33` 和 `0.1` 都是有效的版本号。

比较版本号时，请按从左到右的顺序依次比较它们的修订号。比较修订号时，只需比较 **忽略任何前导零后的整数值** 。也就是说，修订号 `1` 和修订号 `001` **相等** 。如果版本号没有指定某个下标处的修订号，则该修订号视为 `0` 。例如，版本 `1.0` 小于版本 `1.1` ，因为它们下标为 `0` 的修订号相同，而下标为 `1` 的修订号分别为 `0` 和 `1` ，`0 < 1` 。

返回规则如下：

- 如果 `*version1* > *version2*` 返回 `1`，
- 如果 `*version1* < *version2*` 返回 `-1`，
- 除此之外返回 `0`。

 

**示例 1：**

```
输入：version1 = "1.01", version2 = "1.001"
输出：0
解释：忽略前导零，"01" 和 "001" 都表示相同的整数 "1"
```

**示例 2：**

```
输入：version1 = "1.0", version2 = "1.0.0"
输出：0
解释：version1 没有指定下标为 2 的修订号，即视为 "0"
```

**示例 3：**

```
输入：version1 = "0.1", version2 = "1.1"
输出：-1
解释：version1 中下标为 0 的修订号是 "0"，version2 中下标为 0 的修订号是 "1" 。0 < 1，所以 version1 < version2
```

 

**提示：**

- `1 <= version1.length, version2.length <= 500`
- `version1` 和 `version2` 仅包含数字和 `'.'`
- `version1` 和 `version2` 都是 **有效版本号**
- `version1` 和 `version2` 的所有修订号都可以存储在 **32 位整数** 中

![image-20220502215855925](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220502215855925.png)

