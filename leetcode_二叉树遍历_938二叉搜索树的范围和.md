# 938. 二叉搜索树的范围和

## [题目](https://leetcode-cn.com/problems/range-sum-of-bst/)

给定二叉搜索树的根结点 root，返回值位于范围 [low, high] 之间的所有结点的值的和。

## 思路

dfs或bfs均可

## 代码

    # Definition for a binary tree node.
    # class TreeNode:
    #     def __init__(self, val=0, left=None, right=None):
    #         self.val = val
    #         self.left = left
    #         self.right = right
    class Solution:
        
        def rangeSumBST(self, root: TreeNode, low: int, high: int) -> int:
            self.res = 0
            def dfs(root):
                if not root: return
                if root.val >= low and root.val <= high:
                    self.res += root.val
                dfs(root.left)
                dfs(root.right)
            dfs(root)
            return self.res
