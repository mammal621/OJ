# 二维数组中的查找

## [题目](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

## 思路

由于给定的二维数组具备每行从左到右递增以及每列从上到下递增的特点，当访问到一个元素时，可以排除数组中的部分元素。

从二维数组的右上角开始查找。如果当前元素等于目标值，则返回 true。如果当前元素大于目标值，则移到左边一列。如果当前元素小于目标值，则移到下边一行。

可以证明这种方法不会错过目标值。如果当前元素大于目标值，说明当前元素的下边的所有元素都一定大于目标值，因此往下查找不可能找到目标值，往左查找可能找到目标值。如果当前元素小于目标值，说明当前元素的左边的所有元素都一定小于目标值，因此往左查找不可能找到目标值，往下查找可能找到目标值。

1. 若数组为空，返回 false
1. 初始化行下标为 0，列下标为二维数组的列数减 1
1. 重复下列步骤，直到行下标或列下标超出边界
1. 获得当前下标位置的元素 num
   如果 num 和 target 相等，返回 true
   如果 num 大于 target，列下标减 1
   如果 num 小于 target，行下标加 1
1. 循环体执行完毕仍未找到元素等于 target ，说明不存在这样的元素，返回 false`

## 关于不会错过目标值的证明

假设当前检查的位置为(x, y)
共有三种情况：

1. (x, y) == target 此时直接返回true

2. (x, y) > target 由于矩阵的单调性大于y的位置yy上一定有(x, yy) > (x, y)，即任意(x, yy) > target， 因此减小y值等于排除所有(x, yy)位置上的值，不会错过目标值

3. (x, y) < target 由于矩阵的单调性小于x的位置xx上一定有(xx, y) < (x, y)，即任意(xx, y) < target

综上，三种情况下都不会错过目标值

## 代码

    class Solution:
        def findNumberIn2DArray(self, matrix: List[List[int]], target: int) -> bool:
            if not matrix: return False
            x,y = 0, len(matrix[0]) - 1
            while x < len(matrix) and y > -1:
                if matrix[x][y] == target: return True
                if matrix[x][y] > target: y -= 1
                else: x += 1
            return False
