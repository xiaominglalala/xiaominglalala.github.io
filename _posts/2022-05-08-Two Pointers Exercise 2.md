---
layout:     post
title:      Two Pointers Exercise 2
subtitle:   
date:       2022-05-08
author:     Ethan
header-img: img/11.jpg
catalog: true
tags:
    - Leetcode
    - Two Pointers

---
## Two Pointers Exercise 2



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

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/pal1linked-list.jpg)

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

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/160_example_1_1.png)

```
Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3
Output: Intersected at '8'
Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect).
From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,6,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
```

**Example 2:**

![img](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/160_example_2.png)

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