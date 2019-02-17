---
layout: post
title: Weekly Contest 106
category: leetcode
---

### 3 Sum with Multiplicity
```cpp 
class Solution {
public:
    int threeSumMulti(vector<int>& A, int target) {
        constexpr int kMaxN = 100;
    constexpr int kMod = 1e9 + 7;
    vector<long> c(kMaxN + 1, 0);
    for (int a : A) ++c[a];
    long ans = 0;
    for (int i = 0; i <= target; ++i) {
      for (int j = i; j <= target; ++j) {
        const int k = target - i - j;
        if (k < 0 || k >= c.size() || k < j) continue;
        if (!c[i] || !c[j] || !c[k]) continue;
        if (i == j && j == k)
          ans += (c[i] - 2) * (c[i] - 1) * c[i] / 6;
        else if (i == j && j != k)
          ans += c[i] * (c[i] - 1) / 2 * c[k];
        else if (i != j && j == k)
          ans += c[i] * (c[j] - 1) * c[j] / 2;
        else
          ans += c[i] * c[j] * c[k];        
      }
    }
    return ans % kMod;
        
    }
};
```
Another solution adapting the solution above:
```cpp
class Solution {
public:
    int threeSumMulti(vector<int>& A, int target) {
        unordered_map<int, long> c;
        for (int a : A) c[a]++;
        long res = 0;
        for (auto it : c)
            for (auto it2 : c) {
                int i = it.first, j = it2.first, k = target - i - j;
                if (!c.count(k)) continue;
                if (i == j && j == k)
                    res += c[i] * (c[i] - 1) * (c[i] - 2) / 6;
                else if (i == j && j != k)
                    res += c[i] * (c[i] - 1) / 2 * c[k];
                else if (i < j && j < k)
                    res += c[i] * c[j] * c[k];
            }
        return res % int(1e9 + 7);   
    }
};
```

### Minimum Add to Make Parentheses Valid
```cpp
class Solution {
public:
    int minAddToMakeValid(string S) {
        stack<char> leftpar;
        int count = 0;
        for (auto ch : S) {
            if (ch == '(') {
                leftpar.push('(');
            } else {
                if (!leftpar.empty()) {
                    leftpar.pop();
                } else {
                    count ++;
                }
            }
        }
        return count + leftpar.size();
    }
};
```

### Sorty Array by Parity II
```cpp
class Solution {
public:
    vector<int> sortArrayByParityII(vector<int>& A) {
        vector<int> B(A);
        int odd = 1, even = 0;
        for (int i = 0; i < A.size(); i++) {
            if (A[i] % 2 == 1) {
                B[odd] = A[i];
                odd += 2;
            }
            else {
                B[even] = A[i];
                even += 2;
            }
        }
        return B;
    }
};
```