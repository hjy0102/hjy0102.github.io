---
layout: post
title: Is Palindrome
category: leetcode
---

__Number 9 in Leetcode__ and also quite simple.
```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0 || (x != 0 && x % 10 == 0)) {
            return false;
        }
		int sum = 0,temp = x;
		while (x){
			sum = sum * 10 + x % 10;
			x = x / 10;
		}
		return (sum == temp);
    };
};
```

__In similar problems,__ there's #234 Palindrome linked list, which asks given a singly linked list, determine if it is a palindrome in O(n) time and O(1) space.

```cpp
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        stack<int> stk {};
        auto p_node = head;
        
        while (p_node) {
            stk.push(p_node->val);
            
            p_node = p_node->next;
        }
        
        while (head) {
            if (head->val != stk.top() ) return false;
            stk.pop();
            head = head->next;
        }
        return true;
    }
};
```