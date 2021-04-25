# 110平衡二叉树

## 判断是否满足AVL树的条件

## 自顶向下

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
        int height(TreeNode* root) {
            if(root == NULL) return 0;
            else return max(height(root->right), height(root->left))+1;
        }

        bool isBalanced(TreeNode* root) {
            if(root ==NULL) return true;
            else return abs(height(root->right)-height(root->left))<=1 && isBalanced(root->right) && isBalanced(root->left);
        }
    };

## 自下向上

    class Solution {
    public:
        int height(TreeNode* root) {
            if(root == NULL) return 0;
            int left_height = height(root->left);
            int right_height = height(root->right);
            if (left_height==-1||right_height==-1||abs(left_height-right_height)>1) return -1;
            else return max(left_height, right_height) + 1;
        }

        bool isBalanced(TreeNode* root) {
            return height(root)>=0;

        }
    };
