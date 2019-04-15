---
layout: post
title: Longest palindrome
category: trees
tag: leetcode
---

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int sLen = s.length(), maxLen = 0, maxStart = 0;
        int i = 0, l = 0, r = 0, len = 0;
        while(i<=sLen-maxLen/2){
            l = r = i;
            while(r<sLen-1 && s[r+1]==s[r]) r++;
            i = r+1;
            while(l>0 && r<sLen-1 && s[r+1]==s[l-1]) l--, r++;
            len = r-l+1;
            if(maxLen < len) maxLen = len, maxStart = l;
        }
        return s.substr(maxStart, maxLen);
    }
};
```