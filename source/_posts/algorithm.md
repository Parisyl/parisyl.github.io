---
title: 我的算法笔记
tags: [algorithm]
poster:
  topic: Algorithms provide efficient solutions to problems by defining step-by-step procedures.
  headline: Some Algorithm Notes
  color: yellow
date: 2024-03-22 19:22:51
description:
cover: https://f005.backblazeb2.com/file/img-forWeb/uPic/cWP5HR.jpg
banner: https://f005.backblazeb2.com/file/img-forWeb/uPic/cWP5HR.jpg
---

## 有效的括号

[LeetCode](https://leetcode.cn/problems/valid-parentheses/description/) {% mark 简单 color:green %}

### 题目描述
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串 s ，判断字符串是否有效。
有效字符串需满足：
1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。
3. 每个右括号都有一个对应的相同类型的左括号。

示例 1：
输入：s = "()"
输出：true

示例 2：
输入：s = "()[]{}"
输出：true

示例 3：
输入：s = "(]"
输出：false

示例 4：
输入：s = "{[]}"
输出：true

### 解题思路
#### **栈** 
遍历给定的字符串 `s`。当遇到一个左括号时，我们会期望在后续的遍历中，有一个相同类型的右括号将其闭合。由于`后遇到的左括号要先闭合`，因此可以将这个左括号放入栈顶。

当遇到一个右括号时，需要将一个相同类型的左括号闭合。此时，可以取出栈顶的左括号并判断它们是否是相同类型的括号。如果不是相同的类型，或者栈中并没有左括号，那么字符串 `s` 无效，返回 `false`。为了快速判断括号的类型，我们使用`哈希表`存储每一种括号。哈希表的`键`为`右`括号，`值`为相同类型的`左`括号。

在遍历结束后，如果栈中没有左括号，说明字符串 `s` 中的所有左括号闭合，返回 `true`，否则返回 `false`。

注意到有效字符串的长度一定为偶数，因此如果字符串的长度为奇数，可以直接返回 `false`，省去后续的遍历判断过程。

#### 代码实现

```Java
class Solution {
    public boolean isValid(String s) {
        int n = s.length();
        if (n % 2 == 1) {
            return false;
        }
        
        Map<Character, Character> map = new HashMap<>() {{
            put(')', '(');
            put(']', '[');
            put('}', '{');
        }};

        Deque<Character> stack = new LinkedList<Character>();

        for (int i = 0; i < n; i++) {
            char ch = s.charAt(i);
            // 如果ch是 })], 则判断， 否则说明是({[ , 直接入栈
            if (map.containsKey(ch)) {
                if (stack.isEmpty() || stack.peek() != map.get(ch)) {
                    return false;
                }
                stack.pop();
            } else {
                stack.push(ch);
            }
        }
        return stack.isEmpty();
    }
}
```

## 删除排序数组中的重复项
[Leetcode](https://leetcode.cn/problems/remove-duplicates-from-sorted-array/) {% mark 简单 color:green %}

### 题目描述
给你一个**非严格递增排列**的数组`num`，请你原地删除重复出现的元素，使每个元素只出现一次，返回删除后数组的新长度。元素的相对顺序应该保持一致。然后返回`nums`中唯一元素的个数。
考虑`nums`的唯一元素的数量为 `k`，你需要做以下事情确保你的题解可以被通过：
- 更改数组`nums`，使`nums`的前`k`个元素包含唯一元素，并按照它们最初在`nums`中出现的顺序排列。`nums`的其余元素与`nums`的大小不重要。
- 返回`k`。

示例 1：
输入：nums = [1,1,2]
输出：2, nums = [1,2,_]
解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。
示例 2：

输入：nums = [0,0,1,1,1,2,2,3,3,4]
输出：5, nums = [0,1,2,3,4]
解释：函数应该返回新的长度 5 ， 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4 。不需要考虑数组中超出新长度后面的元素。

### 解题思路
#### 双指针

#### 代码实现
```Java
class Solution {
    public int removeDuplicates(int[] nums) {
        int n = nums.length;
        if (n == 0) {
            return 0;
        }
        int fast = 1, slow = 1;
        while (fast < n) {
            if (nums[fast] != nums[fast - 1]) {
                nums[slow] = nums[fast];
                ++slow;
            }
            ++fast;
        }
        return slow;
    }
}

```


## 字符串匹配

[LeetCode](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/) {% mark 简单 color:green %}

### 题目描述
给你两个字符串 haystack 和 needle ，请你在 haystack 字符串中找出 needle 字符串的第一个匹配项的下标（下标从 0 开始）。如果 needle 不是 haystack 的一部分，则返回  -1 。

示例 1：
输入：haystack = "sadbutsad", needle = "sad"
输出：0
解释："sad" 在下标 0 和 6 处匹配。
第一个匹配项的下标是 0 ，所以返回 0 。

示例 2：
输入：haystack = "leetcode", needle = "leeto"
输出：-1
解释："leeto" 没有在 "leetcode" 中出现，所以返回 -1 。
 

### 解题思路
#### 暴力匹配
我们可以让字符串 `needle` 与字符串 `haystack` 的所有长度为 `m` 的子串均匹配一次。

为了减少不必要的匹配，我们每次匹配失败即立刻停止当前子串的匹配，对下一个子串继续匹配。如果当前子串匹配成功，我们返回当前子串的开始位置即可。如果所有子串都匹配失败，则返回 −1。

```Java
class Solution {
    public int strStr(String haystack, String needle) {
        int n = haystack.length(), m = needle.length();
        for (int i = 0; i + m <= n; i++) {
            boolean flag = true;
            for (int j = 0; j < m; j++) {
                if (haystack.charAt(i + j) != needle.charAt(j)) {
                    flag = false;
                    break;
                }
            }
            if (flag) {
                return i;
            }
        }
        return -1;
    }
}

```

#### Knuth-Morris-Pratt算法
Knuth-Morris-Pratt算法，算法，简称 KMP 算法，由 Donald Knuth、James H. Morris 和 Vaughan Pratt 三人于 1977 年联合发表。

Knuth-Morris-Pratt（KMP）算法是一种用于在字符串中查找子字符串的高效算法。它的思路是利用已经匹配过的部分字符信息来避免重复的字符比较，从而实现线性时间复杂度的字符串匹配。

KMP算法的关键在于构建一个部分匹配表（Partial Match Table），用于记录模式串中出现的最长的公共前缀和后缀的长度。通过预处理模式串，KMP算法在匹配过程中利用这个部分匹配表来跳过已经匹配过的字符，从而提高匹配效率。

KMP算法的核心是两个指针：主串指针和模式串指针。在匹配过程中，主串指针向前移动，模式串指针根据部分匹配表来确定下一个匹配位置。当匹配失败时，根据部分匹配表调整模式串指针，从而实现快速跳过不必要的比较。

```Java
class Solution {
    public int strStr(String haystack, String needle) {
        int n = haystack.length(), m = needle.length();
        if (m == 0) {
            return 0;
        }
        int[] pi = new int[m];
        for (int i = 1, j = 0; i < m; i++) {
            while (j > 0 && needle.charAt(i) != needle.charAt(j)) {
                j = pi[j - 1];
            }
            if (needle.charAt(i) == needle.charAt(j)) {
                j++;
            }
            pi[i] = j;
        }
        for (int i = 0, j = 0; i < n; i++) {
            while (j > 0 && haystack.charAt(i) != needle.charAt(j)) {
                j = pi[j - 1];
            }
            if (haystack.charAt(i) == needle.charAt(j)) {
                j++;
            }
            if (j == m) {
                return i - m + 1;
            }
        }
        return -1;
    }
}
```


