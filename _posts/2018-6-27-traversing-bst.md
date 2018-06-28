---
layout: post
title: Traversing Binary Search Trees
category: trees
---

## Preorder Traversal
1. visit the root
2. visit the left subtree
3. visit the right subtree

__The recursive method__
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
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> allNodeValues;
        preorderTrav(root, allNodeValues);
        return allNodeValues;
    }
    
    void preorderTrav(TreeNode *root, vector<int> &allNodeValues) {
        if(!root) return;
        allNodeValues.push_back(root->val);
        preorderTrav(root->left, allNodeValues);
        preorderTrav(root->right, allNodeValues);
        
    }
};
```
__The iterative method__ 
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
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> allNodeValues;
        TreeNode *cur = root;
        stack<TreeNode*> s;
        
        while(cur || !s.empty()) {
            if(!cur) {
                cur = s.top();
                s.pop();
            }
            allNodeValues.push_back(cur->val);
            if(cur->right) s.push(cur->right);
            cur = cur->left;
        }
        
        return allNodeValues;
    }
};
```
## Inorder Traversal
1. visit the left subtree
2. visit the root
3. visit the right subtree

__The recursive method__
```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> nodes;
        inorderHelper(root, nodes);
        return nodes;
    };
    
    void inorderHelper(TreeNode* root, vector<int>& nodes){
        // check for a nullptr root
        if (!root) return;
        // view left subtree
        if(root->left){
            inorderHelper(root->left, nodes);
        }
        // view root node
        nodes.push_back(root->val);
        // view right subtree
        if(root->right){
            inorderHelper(root->right, nodes);
        };
    }
};
```

## Post Order Traversal 
1. visit the left subtree
2. visit the right subtree
3. visit the root


Post order traversal is widely used for mathematical expressions. (e.g 3 4 +) <br>
__The recursive method__
```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> nodes;
        postHelper(root, nodes);
        return nodes;
    };
    
    void postHelper(TreeNode* root, vector<int>& nodes){
        // check for a nullptr root
        if (!root) return;
        // view left subtree
        if(root->left){
            postHelper(root->left, nodes);
        }
        
        // view right subtree
        if(root->right){
            postHelper(root->right, nodes);
        };
        
        // view root node
        nodes.push_back(root->val);
    }
};
```