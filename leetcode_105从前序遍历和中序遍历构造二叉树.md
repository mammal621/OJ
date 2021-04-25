# 105从前序遍历和中序遍历构造二叉树

## 题目

如题

## 代码

    class Solution:
        '''
            1. 位于前序序列首部的元素必定是当前根节点，记为r
            2. 在中序序列中，位于r左边的为r的左子树，位于r右边为右子树
            3. 按上述规则递归
        '''
        def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
            if len(preorder) == 0: return
            if preorder[0] not in inorder: return
            root = TreeNode(preorder[0])
            cur_root = preorder.pop(0)
            root_index = inorder.index(cur_root)
            root.left = self.buildTree(preorder, inorder[:root_index])
            root.right = self.buildTree(preorder, inorder[root_index+1:])

            return root

## 代码2

超时

    class Solution:
        '''
            1. 位于前序序列首部的元素必定是当前根节点，记为r
            2. 在中序序列中，位于r左边的为r的左子树，位于r右边为右子树
            3. 按上述规则递归
        '''
        def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
            if len(preorder) == 0: return
            root = TreeNode(preorder[0])
            cur_root = preorder.pop(0)
            root_index = inorder.index(cur_root)
            cur_left, cur_right = [],[]
            for i in preorder:
                if i in inorder[:root_index]:
                    cur_left.append(i)
                elif i in inorder[root_index+1:]:
                    cur_right.append(i)
            root.left = self.buildTree(cur_left, inorder[:root_index])
            root.right = self.buildTree(cur_right, inorder[root_index+1:])
            return root
