---
layout: post
title: Remove duplicates from a sorted array
category: leetcode
---
# Remove duplicates from a sorted array

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int n = nums.size();
        int count = 1;
        int curr = nums[0];
        for (int i = 1; i < n ; i++ ){
            if(nums[i] != curr){
                nums[count++] = nums[i];
                curr = nums[i];
            }
        }
        return count;
    }
};
```