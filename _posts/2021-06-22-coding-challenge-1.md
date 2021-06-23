---
layout: post
title: Programming Challenge 1<br>Longest Substring Palindrome
featured: true
image: assets/images/coding-challenge.jpeg
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
* $$s_h$$ is a substring of $$s$$ starting from position 1 to $$n$$ - 1 where $$n$$ is the length of $$s$$
* $$s_t$$ is a substring of $$s$$ starting from position 2 to $$n$$
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

## Speed It Up
The main reason that the previous solution exceeds time limit is that generates a lot of duplicate substrings(see picture below for illustration). Moreover, many unnecessary calls have been made. For instance, once we know that `"bab"` is a palindrome, there is no need to find the longest palindrome of `"bad"` because the result won't change the answer. These calls occur a lot in the previous solution which slows the computation down. To speed it up, we have to prevent this waste of computation. However, with the recursive function nature, it is difficult to do such a thing because subcalls cannot know what happen on other branches.

![](/assets/images/coding-challenge-1/duplicate.jpeg)

Therefore, we need to change our solution from recursion to loop. We use nested-loop to generate all possible substrings in which the outer loop represents the start index of the substring and the inner loop represents the end index of the substring. For each substring, check whether it's palindrome and longer than the best answer we found so far.

```
def longest_palindrome(self, s: str) -> str:
    length = len(s)
    longest = ''
    for i in range(length):
        for j in range(i, length):
            ss = s[i:j+1]
            if is_palindrome(ss) and len(ss) > len(longest):
                longest = ss
    
    return longest
```

This code reduce the time complexity to $O(n^2)$ which is significantly better than the previous one. But, we can do even better. Since we keep track of the best answer so far, we can use it to eliminate useless computation in the following scenarios:
* when substring is shorter than the current best answer( $$j$$ - $$i$$ + 1 < $$len(longest)$$).
* when there is no more substring that is longer than the current best answer( $$len(s) - i$$ < $$len(longest)$$).

The final solution looks like this:
```
def longest_palindrome(self, s: str) -> str:
    length = len(s)
    longest = ''
    for i in range(length):
        if length - i < len(longest): break
        for j in range(i, length):
            if j - i + 1 < len(longest): continue
            ss = s[i:j+1]
            if is_palindrome(ss) and len(ss) > len(longest):
                longest = ss
    
    return longest
```

## Conclusion
The challenge of the longest substring palindrome is a huge amount of possible answers which grows exponentially with the length of the input string. The key to solving this question is the elimination of unnecessary computation which reduces the search space that the algorithm has to process.