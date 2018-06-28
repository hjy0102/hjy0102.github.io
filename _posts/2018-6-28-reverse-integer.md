---
layout: post
title: Reverse Integer
category: leetcode
---

```cpp
class Solution {
public:
    int reverse(int x) {
        int rev = 0;
        while (x != 0) {
            rev = rev*10 + x%10;
            x = x/10;
        };
 
        return rev;
    };
};
```