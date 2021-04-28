# 633. 平方数之和

## [题目](https://leetcode-cn.com/problems/sum-of-square-numbers/)

给定一个非负整数 c ，你要判断是否存在两个整数 a 和 b，使得 a^2 + b^2 = c

## 思路1

遍历

根据题目，a与b的取值范围应当在[0, c ** 0.5]之间

从a = 0开始，遍历b，当a^2 + b^2 > c时可停止此轮遍历

## 代码1.1

    class Solution:
        def judgeSquareSum(self, c: int) -> bool:
            for i in range(int(c ** 0.5) + 1):
                for j in range(int(c ** 0.5) + 1):
                    if i * i + j * j == c: return True
                    if i * i + j * j > c: break
            return False

## 思路1.2

直接的两重循环时间复杂度为O(c)，超出时间限制

优化代码，考虑在a固定时，是否存在整数b满足(c - a^2) ** 0.5 = b

## 代码1.2

    class Solution:
        def judgeSquareSum(self, c: int) -> bool:
            for i in range(int(c ** 0.5) + 1):
                    if(c - i * i) ** 0.5 == int((c - i * i) ** 0.5): return True
            return False

## 思路2

双指针

由于 a 和 b 的范围均为 [0, c ** 0.5]，因此可以使用双指针在[0, c ** 0.5]范围进行扫描：

a^2 + b^2 == c: 找到符合条件的 a 和 b，返回 truetrue
a^2 + b^2 < c: 当前值比目标值要小，a++
a^2 + b^2 > c: 当前值比目标值要大，b--

双指针在搜索时，可以理解为马鞍式搜索，故可不重不漏，证明可见
[leetcode题解](https://leetcode-cn.com/problems/sum-of-square-numbers/solution/shuang-zhi-zhen-de-ben-zhi-er-wei-ju-zhe-ebn3/)
[剑指Offer_04二维数组中的查找](https://github.com/mammal621/OJ/blob/main/%E5%89%91%E6%8C%87Offer_04%E4%BA%8C%E7%BB%B4%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E6%9F%A5%E6%89%BE.md)

## 代码2

    class Solution:
        def judgeSquareSum(self, c: int) -> bool:
            a, b = 0, int(c ** 0.5 + 1)
            while a <= b:
                res = a ** 2 + b ** 2
                if res == c: return True
                if res > c: b -= 1
                if res < c: a += 1
            return False

## 思路3

费马平方和定理
