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

[LeetCode](https://leetcode.cn/problems/valid-parentheses/description/) {% mark 简单 color:green %}

### 解题思路
**栈** 
遍历给定的字符串 `s`。当我们遇到一个左括号时，我们会期望在后续的遍历中，有一个相同类型的右括号将其闭合。由于`后遇到的左括号要先闭合`，因此可以将这个左括号放入栈顶。

当遇到一个右括号时，需要将一个相同类型的左括号闭合。此时，可以取出栈顶的左括号并判断它们是否是相同类型的括号。如果不是相同的类型，或者栈中并没有左括号，那么字符串 `s` 无效，返回 `False`。为了快速判断括号的类型，我们使用`哈希表`存储每一种括号。`哈希表`的键为`右`括号，值为相同类型的`左`括号。

在遍历结束后，如果栈中没有左括号，说明字符串 `s` 中的所有左括号闭合，返回 `True`，否则返回 `False`。

注意到有效字符串的长度一定为偶数，因此如果字符串的长度为奇数，可以直接返回 `False`，省去后续的遍历判断过程。

### 代码实现

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


