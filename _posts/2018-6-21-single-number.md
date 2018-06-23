---
layout: post
title: Single number, using XOR
category: leetcode
---

__"Given a non-empty array of integers,__ every element appears twice except for one. Find that single one." was the question prompt and at first glance I thought it was a hash table question but the second piece of the question asks to try to accomplish this task in linear time using *no extra space*.<br>I knew bit-manipulation but someone had to put this into perspective for me to understand the implementation to use bit-manipulation on this question.<br>XOR is a wonderful thing, I learned.<br>
## In C++
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ans = 0;
        for (int i = 0; i < nums.size(); i++ ){
            ans = ans ^ nums[i];
        }
        
        return ans;
    }
};
```
Both solutions are linear time, no extra space needed.
## In javascript
```Javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
    var ans; 
    for (var i = 0 ; i < nums.length ; i++ ){
        ans =  ans ^ nums[i];
    }
    return ans;
};
```