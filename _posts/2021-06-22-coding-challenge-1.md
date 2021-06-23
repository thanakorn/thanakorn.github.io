---
layout: post
title: Programming Challenge 1 - Longest Substring Palindrome
featured: true
image: assets/images/fatos-bytyqi-Agx5_TLsIf4-unsplash.jpeg
author: thanakorn
categories: [ programming ]
---

## Problem Statement
Given a string `s`, return the longest palindromic substring in `s`.<br>*(**Note**: this problem is taken from [LeetCode](https://leetcode.com/problems/longest-palindromic-substring/))*


#### Example 1
```
Input  : "babad"
Output : "bab"
# Note : "aba" is also a valid output.
```

#### Example 2
```
Input  : "cbbd"
Output : "bb"
```

#### Example 3
```
Input  : "abc"
Output : "a"
# Note : "b" and "c" are also a valid output.
```

## First Solution
Suppose `s` equals to `"babad"`, the longest substring of `s` is gonna be either the longest substring of its head, `"baba"`, or its tail, `"abad"`. It can be observed that this problem has a subproblem structure defined as follow:

$$longest\_palin(s) = max(longest\_palin(s_h),longest\_palin(s_t))$$

where
* $$s_t$$ is a substring of $$s$$ starting from position 1 to $$n$$ - 1 where $$n$$ is the length of $$s$$
* $$s_h$$ is a substring of $$s$$ starting from position 2 to $$n$$
* $$longest\_palindrome(s) = s $$ if the length of $$s$$ = 1 or $$s$$ is palindrome.

Therefore, the implementation can be done using a recursive function as shown in the Python code below.

```
def longest_palindrome(s: str) -> str:
    if len(s) == 1 or is_palindrome(s):
        return s

    sh = longest_palindrome(s[:-1])
    st = longest_palindrome(s[1:])
    longest = sh if len(sh) >= len(st) else st
    return longest
```
Even though giving a correct result, this algorithm has $O(2^n)$ time complexity because, for each substring, the fuction makes 2 more calls to itself. Therefore, this solution will exceeds the time limit for a long input string.