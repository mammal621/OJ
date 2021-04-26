# 1011在D天内送达的包裹的能力

## [题目](https://leetcode-cn.com/problems/capacity-to-ship-packages-within-d-days/)

传送带上的包裹必须在 D 天内从一个港口运送到另一个港口。

传送带上的第 i 个包裹的重量为 weights[i]。每一天，我们都会按给出重量的顺序往传送带上装载包裹。我们装载的重量不会超过船的最大运载重量。

返回能在 D 天内将传送带上的所有包裹送达的船的最低运载能力。

## 思路

二分答案

## 代码

    import sys
    class Solution:
        def shipWithinDays(self, weights: List[int], D: int) -> int:
            sum_list = [0] + weights
            for i in range(1, len(sum_list)):
                sum_list[i] = sum_list[i] + sum_list[i - 1]

            def check(ans, days):
                last_index, temp_index, index = 0, 0, 0
                while index < len(sum_list):
                    if sum_list[index] - sum_list[last_index] <= ans:
                        temp_index = index
                        index += 1
                    else:
                        if last_index == temp_index: return False
                        last_index = temp_index
                        days -= 1
                        if days <= 0 : return False
                return True


            low = sum_list[-1] / D - 1
            high = sum_list[-1] + 1
            res = sys.maxsize
            while low < high:
                mid = (low + high) // 2
                flag = check(mid, D)
                if flag: 
                    res = min(mid, res)
                    high = mid
                else: low = mid + 1
            
            return int(res)

## 官方参考代码

    class Solution:
        def shipWithinDays(self, weights: List[int], D: int) -> int:
            # 确定二分查找左右边界
            left, right = max(weights), sum(weights)
            while left < right:
                mid = (left + right) // 2
                # need 为需要运送的天数
                # cur 为当前这一天已经运送的包裹重量之和
                need, cur = 1, 0
                for weight in weights:
                    if cur + weight > mid:
                        need += 1
                        cur = 0
                    cur += weight
                
                if need <= D:
                    right = mid
                else:
                    left = mid + 1
            
            return left
