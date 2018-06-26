---
layout: post
title: Single number (cont'd)
category: leetcode
---

__Like the [two sums]({{ site.baseurl }}/two-sums-contd/) problems,__ Leetcode has variations of the [Single Number]({{ site.baseurl }}/single-number/) problem.

## Single Number II 
__Given a non-empty array of integers, every element appears three times except for one, which appears exactly once. Find that single one.__ This also asks you to accomplish the task in linear time with no extra space.<br>This solution sorts the input array first and compares the set in triples, breaking and returning the last index if the set of three are not equal.<br>The sort algorithm returns nothing, and runs in O(nlogn). There is a solution in linear time using left shifts. You can look it up if you are interested. 
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int i=0;
        while(i<nums.size()){
            if((i+1)>nums.size() || (i+2) > nums.size()) return nums[i]; 
            else if(nums[i] == nums[i+1] && nums[i+1] == nums[i+2]){
                i = i+3;
            }
            else {
                return nums[i];
            }
        }
    }
};
```

## Single Number III

