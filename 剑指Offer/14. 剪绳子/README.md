# 剪绳子

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

```
示例 1：

输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
示例 2:

输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
提示：

2 <= n <= 58
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/jian-sheng-zi-lcof

## 贪心

尽可能分成3，才能使乘积最大。

- 如果除以3余1，那么拆一个1出来，凑成2*2
- 如果除以3余2，那么直接乘以2即可

**复杂度分析**

时间复杂度：O(1)。

空间复杂度：O(1)。

```cpp
class Solution {
public:
    int cuttingRope(int n) {
        if(n <= 3) return n - 1;
        int res = 0, count3 = n / 3;
        if(n % 3 == 0) return pow(3, count3);
        elsae if( n % 3 == 1)
        {
            count3 --;
            return pow(3, count3) * 4;
        }
        else return pow(3, count3) * 2;
    }
};
```