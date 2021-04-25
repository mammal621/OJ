# 461 汉明距离

## 题目

两个整数之间的汉明距离指的是这两个数字对应二进制位不同的位置的数目。

给出两个整数 x 和 y，计算它们之间的汉明距离。

## 代码

### c
    class Solution {
    public:
        int hammingDistance(int x, int y) {
            int count = 0, xx, yy;
            while(0!=x || 0!=y){
                xx = x%2; yy = y%2;
                if(xx!=yy) count++;
                x = x/2; 
                y = y/2;
            }
            return count;
        }
    };

### python
    return bin(x^y).count('1')