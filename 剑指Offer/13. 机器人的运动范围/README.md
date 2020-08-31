# 机器人的运动范围

地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

 
```
示例 1：

输入：m = 2, n = 3, k = 1
输出：3
示例 2：

输入：m = 3, n = 1, k = 0
输出：1
提示：

1 <= n,m <= 100
0 <= k <= 20
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof

## DFS

**复杂度分析**

时间复杂度：O(nm)。每个元素至多访问一次。
空间复杂度：O(nm)。

```cpp
class Solution {
public:
    bool visited[105][105];
    int n, m, k;
    int movingCount(int m, int n, int k) {
        this->n = n;
        this->m = m;
        this->k = k;
        return dfs(0, 0);
    }
    int getNum(int n) {
        int sum = 0;
        while (n > 0) {
            sum += n % 10;
            n /= 10;
        }
        return sum;
    }
    int dfs(int i, int j) {
        // 下标满足条件
        if (i < 0 || i >= m || j < 0 || j >= n ) {
            return 0;
        }
        // 是否访问和满足当前条件
        if (visited[i][j] || getNum(i) + getNum(j) > k) {
            return 0;
        }
        // 标记
        visited[i][j] = true;
        // dfs
        int ans = 1 + dfs(i-1, j) + dfs(i+1, j) + dfs(i, j-1) + dfs(i, j+1);
        return ans;
    }
};
```

## BFS

**复杂度分析**

时间复杂度：O(nm)。每个元素至多访问一次。
空间复杂度：O(nm)。

```cpp
class Solution {
public:
    using pii = pair<int,int>;
    int dir[5] = {-1, 0, 1, 0, -1};
    int movingCount(int m, int n, int k) {
        int visited[m][n];
        memset(visited, -1, sizeof(visited));
        queue<pii> q;
        q.push({0,0});
        visited[0][0] = 1;
        int ret = 0;
        while (!q.empty()) {
            auto node = q.front();
            q.pop();
            ++ret;
            for (int i = 0; i < 4; ++i) {
                int x = node.first + dir[i];
                int y = node.second + dir[i + 1];
                if (x >= 0 && x < m && y >= 0 && y < n && visited[x][y] == -1) {
                    if (getNum(x) + getNum(y) <= k) {
                        q.push({x, y});
                        visited[x][y] = 1;
                    }
                }
            }
        }
        return ret;
    }
    int getNum(int n) {
        int sum = 0;
        while (n > 0) {
            sum += n % 10;
            n /= 10;
        }
        return sum;
    }
};
```