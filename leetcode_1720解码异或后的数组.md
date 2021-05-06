# 1720解码异或后的数组

## [题目](https://leetcode-cn.com/problems/decode-xored-array/)

未知 整数数组 arr 由 n 个非负整数组成。

经编码后变为长度为 n - 1 的另一个整数数组 encoded ，其中 encoded[i] = arr[i] XOR arr[i + 1] 。例如，arr = [1,0,2,1] 经编码后得到 encoded = [1,2,3] 。

给你编码后的数组 encoded 和原数组 arr 的第一个元素 first（arr[0]）。

请解码返回原数组 arr 。可以证明答案存在并且是唯一的。

## 思路(答案存在并且是唯一的推导)

关于异或运算的几条基本定理

异或满足结合律，(a^b)^c = a^(b^c)
异或满足交换律，a^b = b^a
任意数与自身异或得0，a^a = 0
任意数异或0的到自身，a^0 = a
推导过程如下，E[i]表示encoded[i]，A[i]表示arr[i]：

已知 E[i] = A[i] ^ A[i+1]
等式两边同时右异或A[i]，等号仍然成立，E[i] ^ A[i] = A[i] ^ A[i+1] ^ A[i]
由定理1，E[i] ^ A[i] = A[i] ^ (A[i + 1] ^ A[i])
由定理2，E[i] ^ A[i] = A[i] ^ (A[i] ^ A[i+1])
由定理1，E[i] ^ A[i] = (A[i] ^ A[i]) ^ A[i+1]
由定理3，E[i] ^ A[i] = 0 ^ A[i+1]
由定理4，E[i] ^ A[i] = A[i+1]
已知E[i]和A[0]，可得A[1]，同理可得A[2]、A[3]、A[n-1]

来自leetcode用户[Gapex的评论](https://leetcode-cn.com/problems/decode-xored-array/comments/925259)

## 代码

    class Solution:
        def decode(self, encoded: List[int], first: int) -> List[int]:
            ans = [first]
            for i in encoded:
                first = first ^ i
                ans.append(first)
            return ans
