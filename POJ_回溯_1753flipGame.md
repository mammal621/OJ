# filpGame

## 来源

POJ 1753

## [题目](http://poj.org/problem?id=1753)

## 代码

    #define _CRT_SECURE_NO_WARNINGS
    # include<stdio.h>
    # include<string>
    # include<iostream>
    #include <algorithm>

    int ans = 0x3f3f3f3f;
    char map[4][4];

    bool check() // 用于检查是否全部翻转为同一色
    {
        char first = map[0][0];
        for (int i=0; i < 4; i++)
        {
            for (int j = 0; j < 4; j++)
            {
                if (map[i][j] != first) return false;
            }
        }
        return true;
    }

    void turn(int i, int j) // 传入一个位置，用于翻转该块及其周边各块
    {
        // mid
        if (map[i][j] == 'b') map[i][j] = 'w';
        else map[i][j] = 'b';
        // up
        if (i > 0)
        {
            if (map[i-1][j] == 'b') map[i-1][j] = 'w';
            else map[i-1][j] = 'b';
        }
        // down
        if (i < 3)
        {
            if (map[i+1][j] == 'b') map[i+1][j] = 'w';
            else map[i+1][j] = 'b';
        }
        // left
            // down
        if (j > 0)
        {
            if (map[i][j-1] == 'b') map[i][j-1] = 'w';
            else map[i][j-1] = 'b';
        }
        if (j < 3)
        {
            if (map[i][j + 1] == 'b') map[i][j + 1] = 'w';
            else map[i][j +1] = 'b';
        }

    }

    void backtrack(int i, int j, int cur) // 用于回溯
    {
        // 两种停止回溯的条件
        // 1. 成功翻面
        // 2. 最后一行的最后一个被遍历
        if (check()) 
        {
            ans = std::min(ans, cur);  return;
        }
        if (i == 4) return; 

        turn(i, j); // 做出选择
        if (j == 3) backtrack(i+1, 0, cur + 1); // 先遍历每一行,遍历完则换行
        else backtrack(i, j + 1, cur + 1);
        
        turn(i, j); // 撤销选择
        if (j == 3) backtrack(i + 1, 0, cur);
        else backtrack(i, j + 1, cur);
    }

    int main()
    {
        for (int i = 0; i < 4; i++) scanf("%s", map[i]);
        backtrack(0, 0, 0);
        if (ans== 0x3f3f3f3f)
        {
            printf("Impossible\n");
        }
        else
        {
            printf("%d\n", ans);
        }
    }
