# 青蛙跳台阶问题

一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

```
示例 1：

输入：n = 2
输出：2
示例 2：

输入：n = 7
输出：21
提示：

0 <= n <= 100
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof

# 递推
与斐波那契数列思想相同。
**复杂度分析**
时间复杂度：O(n)
空间复杂度：O(1)
```cpp
class Solution {
public:
    const int MAXN = 1e9 + 7;
    int numWays(int n) {
        if (n == 1 || n == 0) {
            return 1;
        } else if (n == 2) {
            return 2;
        } else {
            int f1 = 1;
            int f2 = 2;
            for (int i = 3; i <= n; ++i) {
                int t = f1 + f2;
                t %= MAXN;
                f1 = f2;
                f2 = t;
            }
            return f2;
        }
    }
};
```