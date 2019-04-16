---
layout: post
title: Binary tree right side view
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
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        //Bear typed 
        if (!root) return {};
        
        vector<int> ans = {};
        
        vector<TreeNode*> curr;
        vector<TreeNode*> next;
        
        curr.push_back(root); 
        
        while( !curr.empty() ){
            //add all the children of the nodes in the curr vector into the next vector
            for (auto node : curr) {
                next.push_back(node->left);
                next.push_back(node->right);
            }
            
            // check curr for right most child, add to ans
            ans.push_back(curr.back()-> val);
            // switch next to curr and curr to next
            curr.clear();
            for (auto node : next){
                curr.push_back(node);
            }
            next.clear();
        }
        
        return ans;
    }
};
```

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
    vector<int> rightSideView(TreeNode* root) {
        vector<int> res={};
        if(root==NULL)
            return res;
        vector<TreeNode*> level={root};
        while(level.size()!=0)
        {
            res.push_back(level[level.size()-1]->val);
            int size=level.size();
            for(int i=0;i<size;i++)
            {
                if(level[0]->left!=NULL)
                    level.push_back(level[0]->left);
                if(level[0]->right!=NULL)
                    level.push_back(level[0]->right);
                level.erase(level.begin());
            }
        }
        return res;
    }
    
};
```

```cpp
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> result;
        if(root==NULL)  return result;
        int ans=INT_MIN;
        queue<TreeNode *> q;
        q.push(root);
        q.push(NULL);
        result.push_back(root->val);
        while(!q.empty()){
            TreeNode *temp=q.front();
            q.pop();
            if(temp==NULL) {
                q.push(NULL);
                if(q.front()==NULL) break;
                result.push_back(ans);
            } else {
                if(temp->left) {
                q.push(temp->left);
                ans=temp->left->val;
                }
                if(temp->right){
                    q.push(temp->right);
                    ans=temp->right->val;    
                }
            }
        }
        return result;
    }
}
```

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
    vector<int> rightSideView(TreeNode* root) {
        if(root == NULL)
            return {};
        vector<int> res;
        queue<TreeNode*> myqueue1;
        queue<TreeNode*> myqueue2;
        myqueue1.push(root);
        while(!myqueue1.empty() || !myqueue2.empty()){
            bool flag1 = true;
            while(!myqueue1.empty()){
                if(flag1 == true){
                    res.push_back(myqueue1.back()->val);
                    flag1 = false;
                }
                TreeNode* tmp = myqueue1.front();
                myqueue1.pop();
                if(tmp->left)
                    myqueue2.push(tmp->left);
                if(tmp->right)
                    myqueue2.push(tmp->right);
            }
            bool flag2 = true;
            while(!myqueue2.empty()){
                if(flag2 == true){
                    res.push_back(myqueue2.back()->val);  
                    flag2 = false;
                }
                TreeNode* tmp = myqueue2.front();
                myqueue2.pop();
                if(tmp->left)
                    myqueue1.push(tmp->left);
                if(tmp->right)
                    myqueue1.push(tmp->right);
            }
        }
        return res;
    }
};
```