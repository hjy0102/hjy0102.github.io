---
layout: post
title: Level order transversal of a binary tree
category: trees
tag: leetcode
---

Runs in O(n) time with O(n) space.

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> levelOrder;
        
        if (root == nullptr){
            return levelOrder;
        }
        
        queue<TreeNode*> nodeQ;
        nodeQ.push(root);
        
        while (!nodeQ.empty()) {
            int nodeSize = nodeQ.size();
            vector<int> curLevel;
            
            for (int i = 0; i < nodeSize; i++) {
                TreeNode* topNode = nodeQ.front(); 
                nodeQ.pop();
                curLevel.push_back(topNode->val);
                
                if (topNode->left)
                    nodeQ.push(topNode->left);
                if (topNode->right)
                    nodeQ.push(topNode->right);
            }
            
            levelOrder.push_back(curLevel);
        }
        
        return levelOrder;
    }
};
```