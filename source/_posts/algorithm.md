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



