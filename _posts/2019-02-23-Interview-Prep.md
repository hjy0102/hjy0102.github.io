---
layout: post
title: Feb 2019 Interview Preparation
category: leetcode
---

## Problem 1: extract all leaves from a binary tree in a doubly linked list.

## Problem 2: Given an array arr[], find the maximum j – i such that arr[j] > arr[i].
```java
int max (int x, int y){
    return x > y ? x : y;
}

int min(int x, int y){
    return x < y ? x : y;
}

int maxIndexDiff(int arr[], int n){
    int maxDiff;
    int i, j;

    int RMax[] = new int[n];
    int LMin[] = new int[n];

    // construct LMin such that LMin[i] stores the min value from arr[0] to arr[i]
    LMin[0] = arr[0];
    for (i = 1; i<n; i++){
        LMin[i] = min(arr[i], LMin[i-1]);
    }

    // construct RMax[] such that RMax[j] stores the max value from arr[j] to arr[n-1]
    RMax[n-1] = arr[n-1];
    for (j = n-2; j>=0; j--){
        RMax[j] = max(arr[j], RMax[j+1)]);
    }

    // traverse both arrays from left to right to find optimum j-i *note:similar to mergesort

    i=0; j=0; maxDiff = -1;
    while(j<n && i<n){
        if(LMin[i] < RMax[j]){
            maxDiff = max(maxDiff, j-i);
            j = j+1;
        } else {
            i = i+1;
        }
    }

    return maxDiff;
}
```
Time O(n) space O(n)

## Problem 3: Remove alternate duplicate characters from a char array you have to do it in place i.e. keeping only the odd occurences of each character.

// use two pointer method and bool array of length 256

## Problem 4. In a file of 1 million words, find the 10 most frequent words in that file.

##  Problem 5. Unique Letter String
A character is unique in string S if it occurs exactly once in it.
For example, in string S = "LETTER", the only unique characters are "L" and "R".
Let's define UNIQ(S) as the number of unique characters in string S.
For example, UNIQ("LETTER") =  2.
Given a string S with only uppercases, calculate the sum of UNIQ(substring) over all non-empty substrings of S.
If there are two or more equal substrings at different positions in S, we consider them different.
Since the answer can be very large, return the answer modulo 10 ^ 9 + 7.

```text
Input: "ABC"
Output: 10
Explanation: All possible substrings are: "A","B","C","AB","BC" and "ABC".
Evey substring is composed with only unique letters.
Sum of lengths of all substring is 1 + 1 + 1 + 2 + 2 + 3 = 10
```

```java
class Solution {
    Map<Character, List<Integer>> index;
    int[] peek;
    int N;

    public int uniqueLetterString(String S) {
        index = new HashMap();
        peek = new int[26];
        N = S.length();

        for (int i = 0; i < S.length(); ++i) {
            char c = S.charAt(i);
            index.computeIfAbsent(c, x-> new ArrayList<Integer>()).add(i);
        }

        long cur = 0, ans = 0;
        for (char c: index.keySet()) {
            index.get(c).add(N);
            index.get(c).add(N);
            cur += get(c);
        }

        for (char c: S.toCharArray()) {
            ans += cur;
            long oldv = get(c);
            peek[c - 'A']++;
            cur += get(c) - oldv;
        }
        return (int) ans % 1_000_000_007;
    }

    public long get(char c) {
        List<Integer> indexes = index.get(c);
        int i = peek[c - 'A'];
        return indexes.get(i+1) - indexes.get(i);
    }
}
```
##  Problem 6. Neighbouring cells

```cpp
vector<int> cellCompete(int *states ,int days){
    vector<int> ans;
    for (int i=0; i < days; i++){
        states[-1]=0; //assumptions
        states[8]=0;//assumptions
        int temp[8]; //another array to copy value
        for (int i=-1;i<9;i++){
            temp[i]=states[i]; 
        }
 
        for(int j=0;j<8;j++){
            if(temp[j-1]==temp[j+1]){ 
                states[j]=0; 
            } else{ 
                states[j]=1;
            }
        } 
    }
 
    for (int i=0;i<8;i++){
        ans.push_back(states[i]);
    }
    return ans;
}
```

##  Problem 7. Generalized greated common divisor

```java
// for sorting
import java.util.Arrays;

class GCD
{
    // METHOD SIGNATURE BEGINS, THIS METHOD IS REQUIRED
    public int generalizedGCD(int num, int[] arr)
    {
        // WRITE YOUR CODE HERE
        // first sort the array
        Arrays.sort(arr);
        int ans = arr[0];
        for (int i = 1; i < num; i++){
            ans = gcd(arr[i], ans);
        }
        return ans;
    }
    
    private int gcd(int a, int b){
        if (a==0){
            return b;
        }
        return gcd(b % a, a);
    }
    // METHOD SIGNATURE ENDS
}
```