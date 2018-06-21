---
layout: post
title: Add strings
category: leetcode
---

__This problem showed up as a related problem to [Add two numbers]({{ site.baseurl }}/add-two-numbers)__ and it was relatively quick.
My first attempt was done without much thought but performs decently: better than 66.62% of solutions.
```cpp
class Solution {
public:
    string addStrings(string num1, string num2) {
        string num;
        int length1 = num1.length();
        int length2 = num2.length();
        int carry = 0;

        for (int i = length1 - 1, j = length2 - 1; i >= 0 || j >= 0; i--, j--){
            int temp = 0;
            if (i >= 0) { temp += num1[i] - '0'; }
            if (j >= 0) { temp += num2[j] - '0'; }
            if (carry){ ++temp; }
            carry = temp / 10;
            temp = temp % 10;
            num = char(temp + '0') + num;
        }
        if (carry){
            num = char(carry + '0') + num;
        }
        return num;
    }
};
```
After making a few changes: it performs better than 95.38% of other solutions.
```cpp
class Solution {
public:
    string addStrings(string num1, string num2) {
        string ret;
        for (int i = num1.size() - 1, j = num2.size() - 1, carry = 0; i >= 0 || j >= 0 || carry; i--, j--) {
            int sum = (i >= 0 ? num1[i] - '0' : 0) + (j >= 0 ? num2[j] - '0' : 0) + carry;
            carry = sum / 10;
            ret += sum % 10 + '0';
        }
        reverse(ret.begin(), ret.end());
        return ret;
    }
};
```
Honestly though, it seems like the first solution is far easier to read :) Both were accepted by Leetcode. 