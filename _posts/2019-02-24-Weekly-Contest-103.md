---
layout: post
title: Leetcode Weekly Contest 103
category: leetcode
---

## Smallest Range I
```cpp
class Solution {
public:
    int smallestRangeI(vector<int>& A, int K) {
        int ans;
        
        int _min = *min_element(begin(A), end(A));
        int _max = *max_element(begin(A), end(A));
        
        ans = max(0, (_max - _min) - 2*K );
        
        return ans;
    }
    
    int max(int x, int y){
        return x > y ? x : y;
    }
};
```

## Smallest Range II
```cpp
class Solution {
public:
    int smallestRangeII(vector<int>& A, int K) {
        int n = A.size();
        
        if (n == 1) return 0;
        
        sort(A.begin(), A.end());
        
        int ans = A[n-1] - A[0];
        
        for (int i = 0; i < n-1; i++ ){
            int _max = max(A[n-1], A[i]+ 2*K);
            int _min = min(A[0] +2*K, A[i+1]);
            ans = min(ans, _max - _min);
        }
        
        return ans;
    }
};
```