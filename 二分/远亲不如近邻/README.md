
[远亲不如近邻](https://www.nowcoder.com/practice/1b2c9a2ba11746958036b29f2e9ee72b?tpId=110&&tqId=33454&rp=1&ru=/activity/oj&qru=/ta/job-code/question-ranking)

二分答案，对每个居民找到最小的大于等于该位置的坐标和最大的小于等于该位置的坐标，取最小值为答案。

复杂度分析：

时间复杂度：sort排序复杂度nlog<sub>n</sub>，m次二分查询，每次二分查询复杂度log<sub>n</sub>，总共就是(n+m)log<sub>n</sub>。

空间复杂度：O(n)。

```cpp
class Solution {
public:
    /**
     * 远亲不如近邻
     * @param n int整型 居民个数
     * @param m int整型 方案个数
     * @param a int整型vector 居民的位置
     * @param x int整型vector 方案对应的位置
     * @return int整型vector
     */
    vector<int> solve(int n, int m, vector<int>& a, vector<int>& x) {
        // write code here
        sort(a.begin(), a.end());
        vector<int> v(m);
        for (int i = 0; i < m; ++i) {
            int val = x[i];
            int ans = 2e9;
            // 最大的小于等于x[i]的位置
            if (val < a[0]) {
                ans = a[0] - val;
            } else {
                int l = 0, r = n - 1;
                while (l <= r) {
                    int mid = (l + r) >> 1;
                    if (a[mid] <= val) {
                        ans = min(ans, val - a[mid]);
                        l = mid + 1;
                    } else {
                        r = mid - 1;
                    }
                }
            }
            // 最小的大于等于x[i]的位置
            if (val > a[n-1]) {
                ans = min(ans, val - a[n-1]);
            } else {
                int l = 0, r = n - 1;
                while (l <= r) {
                    int mid = (l + r) >> 1;
                    if (a[mid] >= val) {
                        ans = min(ans, a[mid] - val);
                        r = mid - 1;
                    } else {
                        l = mid + 1;
                    }
                }
            }
            v[i] = ans;
        }
        return v;
    }
};
```