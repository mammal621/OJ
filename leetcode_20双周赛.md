# 第20场双周赛

## [题目1](https://leetcode-cn.com/problems/sort-integers-by-the-number-of-1-bits/)

## 代码1

    class Solution:
        def sortByBits(self, arr: List[int]) -> List[int]:
            arr.sort(key = lambda x:(bin(x).count('1'),x))
            return arr

## [题目2](https://leetcode-cn.com/problems/apply-discount-every-n-orders/)

## 代码2

十分普通的一道题，硬写就能过，然而比赛时leetcode编译会莫名出错，python3全军覆没

    class Cashier:

        def __init__(self, n: int, discount: int, products: List[int], prices: List[int]):
            self.pro = products
            self.pri = prices
            self.isDis = 0
            self.n = n
            self.dis =  (100 - discount) / 100

        def getBill(self, product: List[int], amount: List[int]) -> float:
            self.isDis += 1
            bill = 0
            for i in range(len(product)):
                bill += self.pri[self.pro.index(product[i])] * amount[i]
            return bill if self.isDis % n != 0 else bill * self.dis

## [题目3](https://leetcode-cn.com/problems/number-of-substrings-containing-all-three-characters/)

## 代码3.1

滑动窗口即可，思路一样，循环的次数实际是一致的，然而第一种双重循环的写法会超时

    class Solution:
        def numberOfSubstrings(self, s: str) -> int:
            res = 0
            for i in range(len(s)-2):
                for j in range(i,len(s)):
                    if j == len(s): return res 
                    tmp = s[i:j+1]
                    if 'a' in tmp and 'b' in tmp and 'c' in tmp:
                        res+=len(s)-j
                        break
            return res

## 代码3.2

    class Solution:
        def numberOfSubstrings(self, s: str) -> int:
            i = 0
            j = i+3
            res = 0
            while i < len(s)-2:
                if 'a' in s[i:j] and 'b' in s[i:j] and 'c' in s[i:j]:
                    res += (len(s)-j + 1)
                    i+=1
                    if j < i+3:
                        j = i+3
                else:
                    j+=1
                    if j > len(s):
                        break
            return res

## [题目4](https://leetcode-cn.com/problems/count-all-valid-pickup-and-delivery-options/)

## 代码

高中数学组合

    class Solution:
        def countOrders(self, n: int) -> int:
            if n==1: return 1
            if n==2: return 6
            pre_val = 6
            for i in range(2,n):
                pre_val = pre_val*((2*i+1)*(2*i+2)/2%1000000007)%1000000007
            return int(pre_val)
