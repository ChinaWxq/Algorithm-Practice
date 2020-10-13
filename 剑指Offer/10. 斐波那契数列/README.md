# 斐波那契数列

写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项。斐波那契数列的定义如下：

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

 
```
示例 1：

输入：n = 2
输出：1
示例 2：

输入：n = 5
输出：5
 

提示：

0 <= n <= 100
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof

## 递推

斐波那契数列本质就是一个递推表达式，我们记录中间值即可。

**复杂度分析**

时间复杂度：O(n)

空间复杂度：O(1)
```cpp
class Solution {
public:
    const int MAXN = 1e9 + 7;
    int fib(int n) {
        int f0 = 0;
        int f1 = 1;
        if (n == 0) {
            return f0;
        } else if (n == 1) {
            return f1;
        }
        for (int i = 2; i <= n; ++i) {
            int t = f1 + f0;
            t %= MAXN;
            f0 = f1;
            f1 = t;
        }
        return f1;
    }
};
```