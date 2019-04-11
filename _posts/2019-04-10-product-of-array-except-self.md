---
layout: post
title: Product of Array Except Self
category: leetcode
---

Given an array nums of n integers where n > 1,  return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Example:

Input:  [1,2,3,4]
Output: [24,12,8,6]
Note: Please solve it without division and in O(n).

Follow up:
Could you solve it with constant space complexity? (The output array does not count as extra space for the purpose of space complexity analysis.)

## The division method
This method uses division but still runs in O(n). This is not the answer that this question is looking for however. Also this method does not work if there is a zero in the given array of numbers.

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int prod = 1;
        vector<int> ans;

        for (int i = 0; i < nums.size(); i++ ){
            prod = nums[i] * prod;
        }
        for (int j = 0; j < nums.size(); j++ ){
            ans.push_back(prod/nums[j]);
        }
        
        return ans;
    }
};
```

## Dynamic programming method

If you use dynamic programming, then you can store the left and right products and the value at i will just be the product of the cumulative left product and the cumulative right product.

This solution runs in O(n) but uses O(n) memory. This solution is in the top 30% for runtime.

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        if ( n < 2 ){
            return nums;
        }
        // initialize a vector of n zeros that will store values left to right
        vector<int> leftNums(n, 0);
        //initialize a vector of n zeros that will store values right to left
        vector<int> rightNums(n, 0);
        
        leftNums[0] = nums[0];
        rightNums[n-1] = nums[n-1];
        
        for (int i=1; i< n; i++){
            leftNums[i] = nums[i] * leftNums[i-1];
        }
        
        for (int j=n-2; j >=0; j--){
            rightNums[j] = nums[j] * rightNums[j+1];
        }
        
        vector<int> ans(n, 0);
        
        ans[0] = rightNums[1];
        ans[n-1] = leftNums[n-2];
        
        for (int k = 1; k < n-1; k++ ){
            ans[k] = leftNums[k-1] * rightNums[k+1];
        }
        
        return ans;
    }
};
```

Another solution:

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int len = nums.size();
        int val = 1;
        vector<int> res;
        for(int i = 0; i < len; i++) {
            res.push_back(val);
            val *= nums[i];
        }
        val = 1;
        for(int i = len - 1; i >= 0; i--) {
            res[i] *= val;
            val *= nums[i];
        }
        return res;
    }
};
```