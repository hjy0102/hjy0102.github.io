---
layout: post
title: Serialize and Deserialize BST
category: leetcode
---

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
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        string order; 
        orderDFS(root, order);
        return order;
    }
    
    // traverse dfs tree
    inline void orderDFS(TreeNode* root, string& order){
        if (!root) return;
        char buf[4];
        memcpy(buf, &(root->val), sizeof(int));
        for ( int i=0; i<4; i++){
            order.push_back(buf[i]);
        }
        orderDFS(root->left, order);
        orderDFS(root->right, order);
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        int position = 0;
        return reconstructTree(data, position, INT_MIN, INT_MAX);
    }
    
    // reconstruct tree
    inline TreeNode* reconstructTree(const string& order, int& pos, int minVal, int maxVal){
        if (pos >= order.size()){
            return NULL;
        }
        int value;
        memcpy(&value, &order[pos], sizeof(int));
        if (value < minVal || value > maxVal){
            return NULL;
        }
        TreeNode* node = new TreeNode(value);
        pos += sizeof(int); 
        node->left = reconstructTree(order, pos, minVal, value);
        node->right = reconstructTree(order, pos, value, maxVal);
        return node;
    }
};

// Your Codec object will be instantiated and called as such:
// Codec codec;
// codec.deserialize(codec.serialize(root));
```