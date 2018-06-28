---
layout: post
title: Contains Duplicate III
category: leetcode
---

__Given an array of integers,__ find out whether there are two distinct indices i and j in the array such that the absolute difference between nums[i] and nums[j] is at most t and the absolute difference between i and j is at most k.<br>This solution doesn't handle one edge case: [-INT_MAX, INT_MAX], 1, INT_MAX. 
```cpp
class Solution {
public:
    bool containsNearbyAlmostDuplicate(vector<int>& nums, int k, int t) {
        set<int> window;
        for (int i = 0; i < nums.size(); i++){
            if (i > k){
                window.erase(nums[i-k-1]);
            };
            auto pos = window.lower_bound(nums[i] - t);
            if (pos != window.end() && *pos - nums[i] <= t){
                return true;
            };
            window.insert(nums[i]);
        };
        return false;
    };
};
```
__This adaptation to the code passes all the cases,__ at least the ones in Leetcode. 
```cpp
class Solution {
public:
   bool containsNearbyAlmostDuplicate(vector<int>& nums, int k, int t) {
       set<long long> window;
       for (int i = 0; i < nums.size(); ++i) {
           if (i > k && i - k - 1 < nums.size()){
               window.erase(nums[i - k - 1]);
           };
           auto it = window.lower_bound((long long)nums[i] - t);
           if (it != window.cend() && *it - nums[i] <= t){
               return true;
           };
           window.insert(nums[i]);
       }
       return false;
   };
};
```