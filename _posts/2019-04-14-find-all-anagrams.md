---
layout: post
title: Find all anagrams in a string
category: leetcode
---

### Stack method
```cpp
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        vector<int>res;
        unordered_map<char, int>m;
        for(auto c: p) m[c]++;
        int i = 0, j = 0, count = p.size();
        while(j < s.size()){
            if(m[s[j++]]-- > 0) count--;
            while(count == 0){
                if(j - i == p.size()) res.push_back(i);
                if(m[s[i++]]++ == 0) count++;
            }
        }
        return res;
    }
};
```

### Sliding window method
```cpp
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        
        int _sSize = s.size();
        int _pSize = p.size();
        
        if (_sSize < _pSize) return {};
        
        vector<int> ans;
        
        // instantiate a counter for string s
        vector<int> countS(26,0);
        // instantiate a counter for string p
        vector<int> countP(26,0);
        
        //first window at index 0
        for (int i = 0; i < _pSize; i++){
            countS[s[i] - 'a']++;
            countP[p[i] - 'a']++;
        }
        
        // each window of _pSize is checked if it's an anagram
        for (int j = _pSize; j < _sSize; j++ ){
            // if the two counters are the same, add the starting index
            if (isAnagram(countS, countP)){
                ans.push_back(j-_pSize);
            }
            // update the counter for string s
            countS[s[j] - 'a']++;
            countS[s[j-_pSize] - 'a']--;
        }
        
        // last window to check 
        if (isAnagram(countS, countP)){
            ans.push_back(_sSize - _pSize);
        }
        
        return ans;
    }
    
    // runtime of O(1)
    bool isAnagram(vector<int> countS, vector<int> countP){
        for (int i = 0; i < countP.size(); i++){
            if (countS[i] != countP[i]){
                return false;
            }
        }
        return true;
    }
    
    
};
```