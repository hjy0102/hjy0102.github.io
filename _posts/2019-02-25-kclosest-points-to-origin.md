---
layout: post
title: Feb 2019 Interview Preparation
category: leetcode
---
# K closest points to the origin

```cpp
class Solution {
public:
    class Compare{
    public:
      bool operator()(const vector<int>& a, const vector<int>& b){
          return a[0]*a[0]+a[1]*a[1] > b[0]*b[0]+b[1]*b[1];
      }  
    };
    vector<vector<int>> kClosest(vector<vector<int>>& points, int K) {
        priority_queue<vector<int>,vector<vector<int>>,Compare> q;
        for(auto& x: points){
            q.emplace(x);
        }
        vector<vector<int>> ret;
        for(int i=0;i<K;i++){
            ret.emplace_back(q.top());
            q.pop();
        }
        return ret;
    }
};
```