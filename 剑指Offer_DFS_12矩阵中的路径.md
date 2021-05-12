# 二维数组中的查找

## [题目](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)

给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

## 思路

DFS + 剪枝

## 时间复杂度

时间复杂度 O(M * N * 3^k)

即在最坏情况下，需要将每个位置作为起点(M * N)，遍历可能的所有长度为k的字符串

在任意一点处扩展字符串，在不能走回头路的情况下有三个方向可以选择，故有3^k

## 代码

    class Solution:
        def exist(self, board: List[List[str]], word: str) -> bool:

            # 数组存储可以选择的方向
            add_x = [1, -1, 0, 0]
            add_y = [0, 0, 1, -1]

            # 用visited记录该点处的字符是否被使用过
            visited = [[ 0 for i in range(len(board[0]))] for j in range(len(board))]

            def dfs(x, y, k):
            # 注意这里判断为False的语句出现在了最前面，这样的逻辑下，可以处理k=0时完成匹配，即word长度等于1的情况
                if x < 0 or x >= len(board) or y < 0 or y >= len(board[0]) or visited[x][y] or board[x][y] != word[k]: return False
                if k == len(word) - 1: return True
                visited[x][y] = 1    
                res = False
                for i in range(len(add_x)):
                    res = res or dfs(x + add_x[i], y + add_y[i], k + 1)
                visited[x][y] = 0   
                return res
            
            for i in range(len(board)):
                for j in range(len(board[0])):
                    if board[i][j] == word[0]:
                        if dfs(i, j, 0): return True
            
            return False

## [代码优化](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/solution/mian-shi-ti-12-ju-zhen-zhong-de-lu-jing-shen-du-yo/)

可以在访问后将borad数组上直接修改为特殊值来记录是否已访问

在四个方向上的dfs使用or连接，而不是for循环能更加简洁

python特有的语法可以在越界剪枝时有更简洁的表达

class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        def dfs(i, j, k):
            if not 0 <= i < len(board) or not 0 <= j < len(board[0]) or board[i][j] != word[k]: return False
            if k == len(word) - 1: return True
            board[i][j] = ''
            res = dfs(i + 1, j, k + 1) or dfs(i - 1, j, k + 1) or dfs(i, j + 1, k + 1) or dfs(i, j - 1, k + 1)
            board[i][j] = word[k]
            return res

        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == word[0]:
                    if dfs(i, j, 0): return True
        
        return False
