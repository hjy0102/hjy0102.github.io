---
layout: post
title: Symmetric tree
category: leetcode
---
Given a binary tree, check whether it is a mirror of itself i.e. symmetric around its centre. Bonus points if you can solve it recusively and iteratively. 

### Recursive method
The recursive method would be to check the left branch is the mirror of the right branch throughout the tree.

```cpp
class Solution {
public:
    bool isSymmetric(TreeNode *root) {
        // base case
        if(root == NULL) {
            return true;
        }    
        return isSymmetricHelper(root->left, root->right);
    }

    bool isSymmetricHelper(TreeNode *left, TreeNode *right) {
        // base case
        if(left == NULL && right == NULL) {
            return true;
        } else if(left == NULL || right == NULL) {
            return false;
        }
        // check for the mirror of the value and then the subsequent branches
        return left->val == right->val &&
                isSymmetricHelper(left->right, right->left) &&
                isSymmetricHelper(left->left, right->right);
    }
};
```

### Iterative method
I think the iterative solution is using a queue to load the TreeNodes of one side into it (FIFO) then iterating through the second side and checking the queue for matching values. THis solution would take O(n) time and O(n) memory where there are n TreeNodes in the tree.

```cpp
class Solution {
public:
    bool isSymmetric(TreeNode *root) {
        if (root == NULL) {
            return true;
        }

        if (!root->left && !root->right){
            return true;
        }

        queue<TreeNode*> nodeQ;
        // add the root twice to check if either left or right is null or not
        nodeQ.push(root);
        nodeQ.push(root);
        // pointers to check for symmetry
        TreeNode *leftNode, *rightNode;

        while(!nodeQ.empty()){
            // check the symmetry of the first node

            leftNode = nodeQ.front();
            nodeQ.pop();

            rightNode = nodeQ.front();
            nodeQ.pop();

            // the values of the two nodes are not the same
            if (leftNode->val != rightNode->val){
                return false;
            }

            // otherwise, check left child of the leftNode and the right child of the rightNode
            if (leftNode->left && rightNode->right){
                nodeQ.push(leftNode->left);
                nodeQ.push(rightNode->right);
            } else if (leftNode->left || rightNode->right){
                // this is the case where one branch has more depth than the other
                return false;
            }
            // repeat the check for the right child of the leftNode and the left child of the rightNode
            if (leftNode->right && rightNode->left){
                nodeQ.push(leftNode->right);
                nodeQ.push(rightNode->left);
            } else if (leftNode->right || rightNode->left){
                return false;
            }
        }
        return true;
    }
};
```