---
layout: post
title: Two sum - input sorted in ascending order
category: leetcode
---

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int left = 0;
        int right = numbers.size()-1;

        while (left != right){
            int _sum = numbers[left] + numbers[right];
            if (_sum == target){
                return {left+1, right+1};
            } else if(_sum > target){
                right--;
            } else {
                left++;
            }
        }
        
        return {};
    }
};
```