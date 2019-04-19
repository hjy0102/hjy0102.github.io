---
layout: post
title: Shortest Distance From All Buildings
category: leetcode
---

```cpp
class Solution 
{
public:
    int shortestDistance(vector<vector<int>>& grid) 
    {
        int m = grid.size();
        int n = grid[0].size();
        vector<vector<int>> total_dist(m, vector<int>(n, 0));
        vector<vector<int>> dir = {{0, -1}, {-1, 0}, {0, 1}, {1, 0}};
        int cur = 0; //cur indicates whether the cell has been visited in this time BFS, if grid[x][y] == cur, has not, otherwise has done
        int Min;
        for(int i = 0; i < m; i++)
        {
            for(int j = 0; j < n; j++)
            {
                if(grid[i][j] == 1)
                {
                    Min = -1;
                    queue<pair<int, int>> Queue;
                    Queue.push({i, j});
                    vector<vector<int>> dist(m, vector<int>(n, 0));
                    dist[i][j] = 0;
                    while(Queue.size() > 0)
                    {
                        auto pos = Queue.front();
                        Queue.pop();
                        for(int k = 0; k < 4; k++)
                        {
                            int x = pos.first + dir[k][0];
                            int y = pos.second + dir[k][1];
                            if(x >= 0 && x < m && y >= 0 && y < n && grid[x][y] == cur)
                            {
                                grid[x][y]--; //indicate this cell can not be visited again in this BFS, but availabe for next BFS.
                                dist[x][y] = dist[pos.first][pos.second] + 1;
                                total_dist[x][y] += dist[x][y];
                                Queue.push({x, y});
                                Min = Min == -1 ? total_dist[x][y] : min(Min, total_dist[x][y]); //only the last time works, previous Min will be overwrote in next BFS
                            }
                                
                        }
                    }
                    cur--;
                }
            }
        }
        return Min;
    }
};
```

```cpp
class Solution {
public:
    int shortestDistance(vector<vector<int>>& grid) {
        const int row = grid.size();
        
        if( row == 0 ) return -1;
        const int col = grid[0].size();
        
        int myBuilding = 0;
        int ans = INT_MAX;
        // directions we can travel down, up, left, right
        const vector<pair<int,int>> dirs = {{-1,0}, {1,0}, {0,-1}, {0, 1}};
        
        vector<vector<int>> dist(row, vector<int>(col, 0));
        vector<vector<int>> reach(row, vector<int>(col, 0));
        
        for (int i = 0; i< row; i++ ){
            for (int j = 0; j< col; j++){
                // house is found
                if (grid[i][j] == 1){
                    myBuilding++;
                    int distance = 0;
                    
                    vector<vector<bool>> visited(row, vector<bool>(col, false));
                    queue<pair<int, int>> curLevel, nextLevel;
                    curLevel.emplace(i, j);
                    while(!curLevel.empty()){
                        distance++;
                        while(!curLevel.empty()){
                            pair<int,int> cur = curLevel.front();
                            curLevel.pop();
                            int x = cur.first;
                            int y = cur.second;
                            reach[x][y]++;
                            for(auto dir : dirs){
                                int i = x + dir.first, j = y + dir.second;
                                // if you haven't visited before, it's an empty space & in bounds
                                if( i >= 0 && i < row && j >= 0 && j < col && !visited[i][j] 
                                   && grid[i][j] == 0 ){
                                    dist[i][j] += distance;
                                    nextLevel.emplace(i,j);
                                    visited[i][j]=true;
                                }
                            }
                        }
                        swap(curLevel, nextLevel);
                    }
                }
            }
        }
            for(int i = 0; i < row; i++){
                for(int j = 0; j<col; j++){
                    if (grid[i][j]==0 && reach[i][j]==myBuilding){
                            ans=min(ans, dist[i][j]);
                    }
                }
            }
        
    return ans == INT_MAX ? -1 : ans;
    }
};
```