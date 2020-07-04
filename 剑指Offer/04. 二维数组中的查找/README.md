# 二维数组中的查找

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

 

**示例:**

```
现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。
给定 target = 20，返回 false。
```

**限制：**

`0 <= n <= 1000`

`0 <= m <= 1000`

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof

## 解法

### 暴力搜索

拿到题目，就想到了直接暴力搜索，由于每一行、每一列是递增的顺序，就可以暴力从行开始搜索。

时间复杂度O(n<sup>2</sup>)，空间复杂度O(1)。

```cpp
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        for (int i = 0; i < matrix.size(); ++i) {
            for (int j = 0; j < matrix[i].size(); ++j) {
                if (matrix[i][j] == target) {
                    return true;
                }
            }
        }
        return false;
    }
};
```

### 规律搜索

每一行从左往右递增，每一列从下往上递增。左下角的数是m行，n列中最小的数。

搜索过程：以左下角的数为基准

- 如果比target的小，列数增加再重复过程
- 如果比target的大，行数减小再重复过程
- 如果与target一样大，返回true

### 复杂度分析

时间复杂度：O(n+m)。在循环语句中，除非直接返回结果否则每一次行会减少或者列增加一次，矩阵共有m行n列，因此在循环截止之前会执行至多m+n次。

空间复杂度：O(1)。没有额外的存储空间。

```cpp
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        if (matrix.size() == 0) {
            return false;
        }
        int rows = matrix.size();
        int cols = matrix[0].size();
        int row = rows - 1, col = 0;
        while (row >= 0 && col < cols)
        {
            if (matrix[row][col] > target)
            {
                row--;
            }
            else if (matrix[row][col] < target)
            {
                col++;
            }
            else
            {
                return true;
            }
        }
        return false;
    }
};
```

