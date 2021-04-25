# Radar Installation

## [题目](http://poj.org/problem?id=1328)

## 思路

1. 对于每个小岛的坐标，可以计算出能覆盖到它的最右侧雷达和最左侧雷达坐标
2. 将所有小岛对应的雷达坐标进行排序
3. 从最左侧小岛开始，若第二个小岛的对应的最左侧雷达坐标大于第一个小岛最右侧雷达坐标，则说明需要增加一个雷达，否则与第一个小岛使用同一个雷达即可，依次比较

## 代码

    #include<iostream>
    #include<algorithm>
    using namespace std; // 使用标准库


    struct node // 用于表示小岛与雷达坐标的结构体
    {
        double l;
        double r;
    }nodes[1001];

    bool cmp(node a, node b) // 比较小岛位置的比较函数
    {
        if (a.r == b.r) return a.l > b.l;
        return a.r < b.r;
    }

    int main()
    {
        int n, d, cnt = 0;
        double x, y;
        while (true)
        {
            cin >> n >> d;
            if (!n) break;
            bool flag = d >= 0;
            for (int i = 0; i < n; i++)
            {
                cin >> x >> y;
                flag = flag && y <= d;
                if (flag)
                {
                    nodes[i].l = x - sqrt(d * d - y * y);
                    nodes[i].r = x + sqrt(d * d - y * y);
                }
            }
            sort(nodes, nodes + n, cmp);
            int res = -1;
            if (flag)
            {
                res = 1;
                double maxr = nodes[0].r;
                for (int i = 0; i < n; ++i)
                {
                    if (nodes[i].l > maxr)
                    {
                        maxr = nodes[i].r;
                        ++res;
                    }
                }
            }
            cout << "Case" << ++cnt << ": " << res << endl;
        }
    }
