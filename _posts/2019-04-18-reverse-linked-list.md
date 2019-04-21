---
layout: post
title: Reverse Linked List
category: trees
tag: leetcode
---

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* curr = NULL;
        while(head) {
            ListNode* next = head->next;
            head->next = curr;
            curr = head; 
            head = next;
        }
        return curr;
    }
};
```