# 12整数转罗马数字

## [题目](https://leetcode-cn.com/problems/integer-to-roman/)

给你一个整数，将其转为罗马数字。

## 思路

根据罗马数字规则（见原题目）模拟即可

## 代码

    class Solution:
        def intToRoman(self, num: int) -> str:
            dic = [
            (1000, "M"),
            (900, "CM"),
            (500, "D"),
            (400, "CD"),
            (100, "C"),
            (90, "XC"),
            (50, "L"),
            (40, "XL"),
            (10, "X"),
            (9, "IX"),
            (5, "V"),
            (4, "IV"),
            (1, "I"),
        ]
            res = list()
            for value, symbol in dic:
                while num >= value:
                    num -= value
                    res.append(symbol)
                if num == 0:
                    break
            return "".join(res)
