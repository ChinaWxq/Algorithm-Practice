# 16. 数值的整数次方

实现函数double Power(double base, int exponent)，求base的exponent次方。不得使用库函数，同时不需要考虑大数问题。
 
```
示例 1:

输入: 2.00000, 10
输出: 1024.00000
示例 2:

输入: 2.10000, 3
输出: 9.26100
示例 3:

输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25

说明:

-100.0 < x < 100.0
n 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof

## 快速幂

![](./show.png)

![](./show2.png)



```cpp
class Solution {
public:
    double myPow(double x, int n) {
        if (x == 0) {
            return 0; // 避免 1 / x 错误
        }
        long power = n;
        if (power < 0) { // 如果是负数，底数要变
            power = -power;
            x = 1 / x;
        }
        double result = 1.0;
        while (power > 0) {
            if (power & 1) { // 如果power是奇数
                result *= x; // 更新result
            }
            power >>= 1; // power / 2
            x *= x; // 更新底数
        }
        return result;
    }
};
```