---
layout: post
title: License Key Formatting
category: leetcode
---

```cpp
class Solution {
public:
    
    string licenseKeyFormatting(string S, int K) {
        
        // remove dashes and capitalize lowercase characters
        for(int i = 0; i < S.size(); i++) {
            if(S[i] == '-') { S.erase(i, 1); i--; }
            else if(islower(S[i])) { S[i] = toupper(S[i]); }
        }

        // store number of dashes inserted to offset index
        int num_dashes = 0;
        int index = 1;
        
        // insert dashes from right to left
        for(int j = S.size() - 1; j > 0; j--) {
            if((index % K) == 0) { S.insert(j, 1, '-'); }
            index++;
        }
        
        return S;

    }
    
};
```