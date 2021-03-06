---
layout: post
title: Two city scheduling 
category: trees
tag: leetcode contest
---
```cpp
int twoCitySchedCost(vector<vector<int>>& cs, int res = 0) {
  sort(begin(cs), end(cs), [](vector<int> &v1, vector<int> &v2) {
    return (v1[0] - v1[1] < v2[0] - v2[1]);
  });
  for (auto i = 0; i < cs.size() / 2; ++i) {
    res += cs[i][0] + cs[i + cs.size() / 2][1];
  }
  return res;
}
```
Runtime: O(n log n). We sort the array then go through it once.
Memory: O(1). We sort the array in-place.