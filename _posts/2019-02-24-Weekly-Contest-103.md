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

## Snakes and Ladders
```cpp
class Solution {
public:
    int snakesAndLadders(vector<vector<int>>& board) {
        int N = board.size();
        
        if (N == 1) return 0;
        
        // keep track of where you've been on the board
        unordered_map<int, int> lookup;
        lookup[1] = 0;
        queue<int> q({1});
        while( !q.empty() ){
            auto s = q.front();
            q.pop();
            
            if (s == N * N) {
                return lookup[s];
            }
            
            for (int i = s +1; i < min(s+6, N*N)+1; i++){
                int row, column;
                int s2 = i;
                tie(row, column) = coordinate(N, i);
                
                if(board[row][column] != -1){
                    s2 = board[row][column];
                }
                if(!lookup.count(s2)){
                    lookup[s2] = lookup[s]+1;
                    q.emplace(s2);
                }
            }
        }
        
        return -1;
    }
    
private:
    pair<int, int> coordinate(int n, int b){
        const int a = (b - 1)/ n;
        const int k = (b - 1) % n;
            
        const int r = n - 1 - a;
        const int c = (r % 2 != n  % 2) ? k : (n - 1 - k);
        return {r, c};
    }
    
};
```

## Online Election
