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
        if(nums.size()==1 || nums.size()==0)
            return nums.size();
        int count = 0;
        for(int i=0; i < nums.size()-1 ;i++){
            if(nums[i]!=nums[i+1]){
                nums[count++] = nums[i];
            }
        }
        nums[count++] = nums[nums.size() - 1];
        return count;
    }
};
```