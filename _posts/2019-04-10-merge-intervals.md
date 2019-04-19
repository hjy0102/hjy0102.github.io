---
layout: post
title: Merge intervals
category: leetcode
---

### using a vector of ints as a pair
```cpp
class Solution {
public:

    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        if (intervals.empty()){
            return intervals;
        }
        
        // sort the intervals by comparing their first values using lambda function
        sort(intervals.begin(), intervals.end(), 
             [](vector<int> a, vector<int> b){
                return a.front() < b.front();    
                });
        
        vector<vector<int>> ans;
        ans.push_back(intervals[0]);
        // intervals is now a sorted array with the smallest first value in the beginning
        for (int i = 1; i < intervals.size(); i++ ){
            if ( intervals[i].front() <= ans.back().back() ){
                vector<int> temp = {
                                        ans.back().front(), 
                                        max(ans.back().back(), intervals[i].back())
                                    };
                ans.pop_back();
                ans.push_back(temp);
            } else {
                ans.push_back(intervals[i]);
            }
        }
        return ans;
    }
};
```


### using an Interval struct
```cpp
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
class Solution {
public:
    static bool compInterval(Interval a, Interval b){
        return a.start < b.start;
    }
    
    vector<Interval> merge(vector<Interval>& intervals) {
        //base case: empty vector of intervals
        if (intervals.empty()){
            return intervals;
        };
        // sort from the first 
        sort(intervals.begin(), intervals.end(), compInterval);
        
        vector<Interval> ans;
        ans.push_back(intervals[0]);
        
        for (int i = 1; i <intervals.size(); i++){
            if (intervals[i].start <= ans.back().end){
                Interval temp(ans.back().start, max( ans.back().end, intervals[i].end));
                ans.pop_back();
                ans.push_back(temp);
            } else {
                ans.push_back(intervals[i]);
            }
        }
        return ans;
    }
    
    
};
```