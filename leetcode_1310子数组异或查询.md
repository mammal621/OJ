# 1310. 子数组异或查询

## [题目](https://leetcode-cn.com/problems/xor-queries-of-a-subarray/)

有一个正整数数组 arr，现给你一个对应的查询数组 queries，其中 queries[i] = [Li, Ri]。

对于每个查询 i，请你计算从 Li 到 Ri 的 XOR 值（即 arr[Li] xor arr[Li+1] xor ... xor arr[Ri]）作为本次查询的结果。

并返回一个包含给定查询 queries 所有结果的数组。

## 思路

前缀和的思想

## 代码

class Solution:
    def xorQueries(self, arr: List[int], queries: List[List[int]]) -> List[int]:
        ans = []
        for i in range(1, len(arr)):
            arr[i] ^= arr[i-1]
        for j in queries:
            if j[0] == 0: ans.append(arr[j[1]])
            else: ans.append(arr[j[1]] ^ arr[j[0] - 1])
        return ans
