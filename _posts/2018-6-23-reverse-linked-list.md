---
layout: post
title: Reverse Linked List
category: leetcode
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
        if(head==NULL)
            return NULL; // for null pointer situation
        
        ListNode* p=head,*q=head->next,*r;
        
        while(q!=NULL){
            r=q->next;
            q->next=p;
            p=q;
            q=r;
        }
        head->next=NULL;
        
        return p;
        
    }
};
```