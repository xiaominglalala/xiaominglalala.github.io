---
layout:     post
title:      Hash Table (Updating)
subtitle:   
date:       2022-04-05
author:     Ethan
header-img: img/landscape_0.jpg
catalog: true
tags:
    - Leetcode
    - Hash Table
---

## 哈希表

哈希表是根据关键码的值而直接进行访问的数据结构。

#### [242. 有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/) & [剑指 Offer II 032. 有效的变位词](https://leetcode-cn.com/problems/dKk3P7/)

难度简单472

给定两个字符串 `*s*` 和 `*t*` ，编写一个函数来判断 `*t*` 是否是 `*s*` 的字母异位词。

**注意：**若 `*s*` 和 `*t*` 中每个字符出现的次数都相同，则称 `*s*` 和 `*t*` 互为字母异位词。

 

**示例 1:**

```
输入: s = "anagram", t = "nagaram"
输出: true
```

**示例 2:**

```
输入: s = "rat", t = "car"
输出: false
```

思路：

- 定义一个数组叫做record用来上记录字符串s里字符出现的次数
- 把字符映射到哈希表的索引下标上，**因为字符a到字符z的ASCII是26个连续的数值，所以字符a映射为下标0，相应的字符z映射为下标25**
- 那看一下如何检查字符串t中是否出现了这些字符，同样在遍历字符串t的时候，对t中出现的字符映射哈希表索引上的数值再做-1的操作
- **record数组如果有的元素不为零0，说明字符串s和t一定是谁多了字符或者谁少了字符，return false。**
- 最后如果record数组所有元素都为零0，说明字符串s和t是字母异位词，return true
- 时间复杂度为O(n), 空间复杂度为O(1)

代码：

- 获得字母的顺序是ord()
- ![image-20220410011836230](https://raw.githubusercontent.com/xiaominglalala/pic/main/img/image-20220410011836230.png)

#### [349. 两个数组的交集](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

难度简单458

给定两个数组，编写一个函数来计算它们的交集。

 

**示例 1：**

```
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2]
```

**示例 2：**

```
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[9,4]
```

思路：

代码：



#### [202. 快乐数](https://leetcode-cn.com/problems/happy-number/)

难度简单760

编写一个算法来判断一个数 `n` 是不是快乐数。

「快乐数」定义为：

- 对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。
- 然后重复这个过程直到这个数变为 1，也可能是 **无限循环** 但始终变不到 1。
- 如果 **可以变为** 1，那么这个数就是快乐数。

如果 `n` 是快乐数就返回 `true` ；不是，则返回 `false` 。

 

**示例 1：**

```
输入：n = 19
输出：true
解释：
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

**示例 2：**

```
输入：n = 2
输出：false
```

####  [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

思路：

- 如果使用暴力解法，将会是O(n^2)的时间复杂度。所以我们使用hash table来不断查询target - x[i]是不是一个hash table存储过的值，并将x[i]插入hash table
  - 如果是，返回hash table[target - x[i]], 也就是对应的键，也就是位置。还有位置i
  - 如果不是，就下一轮
  - 记住如果没有匹配的要返回空的[]
  - 注意初始化table = dict() 是(), 不是{}
  - 注意hash table[value] = key(位置)

代码：

#### [454. 四数相加 II](https://leetcode-cn.com/problems/4sum-ii/)

难度中等467

给你四个整数数组 `nums1`、`nums2`、`nums3` 和 `nums4` ，数组长度都是 `n` ，请你计算有多少个元组 `(i, j, k, l)` 能满足：

- `0 <= i, j, k, l < n`
- `nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`

 

**示例 1：**

```
输入：nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
输出：2
解释：
两个元组如下：
1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0
```

**示例 2：**

```
输入：nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
输出：1
```

#### [383. 赎金信](https://leetcode-cn.com/problems/ransom-note/)

难度简单259

给你两个字符串：`ransomNote` 和 `magazine` ，判断 `ransomNote` 能不能由 `magazine` 里面的字符构成。

如果可以，返回 `true` ；否则返回 `false` 。

`magazine` 中的每个字符只能在 `ransomNote` 中使用一次。

 

**示例 1：**

```
输入：ransomNote = "a", magazine = "b"
输出：false
```

**示例 2：**

```
输入：ransomNote = "aa", magazine = "ab"
输出：false
```

**示例 3：**

```
输入：ransomNote = "aa", magazine = "aab"
输出：true
```

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



难度中等4142

给你一个包含 `n` 个整数的数组 `nums`，判断 `nums` 中是否存在三个元素 *a，b，c ，*使得 *a + b + c =* 0 ？请你找出所有和为 `0` 且不重复的三元组。

**注意：**答案中不可以包含重复的三元组。

 

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

#### 146. LRU 缓存机制 & [剑指 Offer II 031. 最近最少使用缓存](https://leetcode-cn.com/problems/OrIXps/)

运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制 。
实现 LRUCache 类：

LRUCache(int capacity) 以正整数作为容量 capacity 初始化 LRU 缓存
int get(int key) 如果关键字 key 存在于缓存中，则返回关键字的值，否则返回 -1 。
void put(int key, int value) 如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组「关键字-值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。


进阶：你是否可以在 O(1) 时间复杂度内完成这两种操作？

示例：

输入
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
输出
[null, null, null, 1, null, -1, null, -1, 3, 4]

解释
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // 缓存是 {1=1}
lRUCache.put(2, 2); // 缓存是 {1=1, 2=2}
lRUCache.get(1);    // 返回 1
lRUCache.put(3, 3); // 该操作会使得关键字 2 作废，缓存是 {1=1, 3=3}
lRUCache.get(2);    // 返回 -1 (未找到)
lRUCache.put(4, 4); // 该操作会使得关键字 1 作废，缓存是 {4=4, 3=3}
lRUCache.get(1);    // 返回 -1 (未找到)
lRUCache.get(3);    // 返回 3
lRUCache.get(4);    // 返回 4


提示：

1 <= capacity <= 3000
0 <= key <= 10000
0 <= value <= 105
最多调用 2 * 105 次 get 和 put

------

思路：

- 在 Python 语言中，有一种结合了哈希表与双向链表的数据结构 OrderedDict，只需要短短的几行代码就可以完成本题。在 Java 语言中，同样有类似的数据结构 LinkedHashMap
- 双向链表`DLinkedNode`存储了node的键值对，前一个是谁，后一个是谁。每一个node都是一个DLinkedNode
  ![image-20211117115628790](C:\Users\BenWong\AppData\Roaming\Typora\typora-user-images\image-20211117115628790.png)
- 使用Python的dict()来实现Hash map用于缓存数据的key来映射链表中的位置
- 所以我们用哈希表来定位，找到链表里的位置，然后移到头部
- 对于get操作，首先在hash map中看key是否存在
  - 如果不存在，则返回-1；
  - 如果存在，则用hash map定位key在链表中的对应的位置，将他移到最前面，然后返回他的值
- 对于put操作，首先在hash map 看key是否存在
  - 如果不存在，则创建一个node加入链表的头部。看是否超出容量，如果超出，删除链表的尾部节点
  - 如果存在，则用hash map定位key在链表中的对应位置，将他移动到最前面，再修改他的值

代码：

#### 953. [验证外星语词典](https://leetcode-cn.com/problems/verifying-an-alien-dictionary/)(verifying-an-alien-dictionary) & [剑指 Offer II 034. 外星语言是否排序](https://leetcode-cn.com/problems/lwyVBB/)

某种外星语也使用英文小写字母，但可能顺序 order 不同。字母表的顺序（order）是一些小写字母的排列。

给定一组用外星语书写的单词 words，以及其字母表的顺序 order，只有当给定的单词在这种外星语中按字典序排列时，返回 true；否则，返回 false。

 

示例 1：

>输入：words = ["hello","leetcode"], order = "hlabcdefgijkmnopqrstuvwxyz"
>输出：true
>解释：在该语言的字母表中，'h' 位于 'l' 之前，所以单词序列是按字典序排列的。

示例 2：

>输入：words = ["word","world","row"], order = "worldabcefghijkmnpqstuvxyz"
>输出：false
>解释：在该语言的字母表中，'d' 位于 'l' 之后，那么 words[0] > words[1]，因此单词序>列不是按字典序排列的。

示例 3：

>输入：words = ["apple","app"], order = "abcdefghijklmnopqrstuvwxyz"
>输出：false
>解释：当前三个字符 "app" 匹配时，第二个字符串相对短一些，然后根据词典编纂规则 "apple" > "app"，因为 'l' > '∅'，其中 '∅' 是空白字符，定义为比任何其他字符都小（更多信息）。


------

思路：

-  Python字典的底层实现是哈希表，所以我们使用字典来存储order的数据
-  字典序比较的时候，只有前面的字符等时才会比较后面的字符的大小。**第一个示例第一个字符的比较结果就可以确定整个字符串的大小关系**，不需要再考虑后面的字符。
-  我们比较的是相邻的两个单词，一旦出现顺序错误，则报错
-  对于比较，我们分两类讨论：
   - 两个单词长度不同，但是出现的部分都是重合的，比如apple和app。由于app比apple短，所以app必须在apple前面，即app <= apple
   - 如果两个单词没到任何一个人的尾部，就已经出现不同，则检查这个是否符合order顺序吗。直到出现不符，否则为True
-  字典哈希表的实现方式：`order_index = {c: i for i, c in enumerate(order)}`注意是值对应键，因为我们查找时是用字母值查找对应的顺序
-  注意要break来终止后续的比较, 发现第一位不相等，如果符合顺序就break，去看长度不比较后面的。如果不符合顺序，就return False
-  for else是如果for顺利完再会执行else，如果由于return 和break中断，则不会执行else

代码：

#### [380. O(1) 时间插入、删除和获取随机元素](https://leetcode-cn.com/problems/insert-delete-getrandom-o1/) & [剑指 Offer II 030. 插入、删除和随机访问都是 O(1) 的容器](https://leetcode-cn.com/problems/FortPu/)

难度中等459

实现`RandomizedSet` 类：

- `RandomizedSet()` 初始化 `RandomizedSet` 对象
- `bool insert(int val)` 当元素 `val` 不存在时，向集合中插入该项，并返回 `true` ；否则，返回 `false` 。
- `bool remove(int val)` 当元素 `val` 存在时，从集合中移除该项，并返回 `true` ；否则，返回 `false` 。
- `int getRandom()` 随机返回现有集合中的一项（测试用例保证调用此方法时集合中至少存在一个元素）。每个元素应该有 **相同的概率** 被返回。

你必须实现类的所有函数，并满足每个函数的 **平均** 时间复杂度为 `O(1)` 。

 

**示例：**

```
输入
["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]
[[], [1], [2], [2], [], [1], [2], []]
输出
[null, true, false, true, 2, true, false, 2]

解释
RandomizedSet randomizedSet = new RandomizedSet();
randomizedSet.insert(1); // 向集合中插入 1 。返回 true 表示 1 被成功地插入。
randomizedSet.remove(2); // 返回 false ，表示集合中不存在 2 。
randomizedSet.insert(2); // 向集合中插入 2 。返回 true 。集合现在包含 [1,2] 。
randomizedSet.getRandom(); // getRandom 应随机返回 1 或 2 。
randomizedSet.remove(1); // 从集合中移除 1 ，返回 true 。集合现在包含 [2] 。
randomizedSet.insert(2); // 2 已在集合中，所以返回 false 。
randomizedSet.getRandom(); // 由于 2 是集合中唯一的数字，getRandom 总是返回 2 。
```

#### [49. 字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/) & [剑指 Offer II 033. 变位词组](https://leetcode-cn.com/problems/sfvd7V/)

难度中等1092

给你一个字符串数组，请你将 **字母异位词** 组合在一起。可以按任意顺序返回结果列表。

**字母异位词** 是由重新排列源单词的字母得到的一个新单词，所有源单词中的字母通常恰好只用一次。

 

**示例 1:**

```
输入: strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
输出: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

**示例 2:**

```
输入: strs = [""]
输出: [[""]]
```

**示例 3:**

```
输入: strs = ["a"]
输出: [["a"]]
```

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

#### 
