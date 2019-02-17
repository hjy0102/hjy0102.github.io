---
layout: post
title: Maximum depth of a binary tree
category: leetcode
---

Given a binary tree, find its maximum depth.

Solved recursively:
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        int depth = 0;
        if (!root) {
            return depth;
        } else {
            depth++;
            return max(maxDepthHelper(root->left, depth), maxDepthHelper(root->right, depth));
        }
        return depth;
    }
    
    int maxDepthHelper(TreeNode* root, int depth){
        if (!root) {
            return depth;
        }
        depth++;
        return max(maxDepthHelper(root->left, depth), maxDepthHelper(root->right, depth));
        
    }
};
```