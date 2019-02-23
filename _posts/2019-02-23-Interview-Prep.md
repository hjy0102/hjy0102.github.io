---
layout: post
title: Feb 2019 Interview Preparation
category: leetcode
---

Problem: extract all leaves from a binary tree in a doubly linked list.

Problem: Given an array arr[], find the maximum j – i such that arr[j] > arr[i].

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

