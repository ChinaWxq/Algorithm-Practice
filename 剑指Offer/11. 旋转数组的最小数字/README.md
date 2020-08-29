# 旋转数组的最小数字

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  

```
示例 1：

输入：[3,4,5,1,2]
输出：1
示例 2：

输入：[2,2,2,0,1]
输出：0
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof

## 暴力查找

一个递增排序的序列，前n个元素移到数组的末尾，从下标0开始查找如果`a[i+1] < a[i]`那么证明`a[i + 1]`为未旋转数组的首元素，如果未找到，则说明整个序列旋转，首元素仍是答案。

**复杂度分析**
时间复杂度：O(n)。

空间复杂度：O(1)。

```cpp
class Solution {
public:
    int minArray(vector<int>& numbers) {
        int len = numbers.size();
        for (int i = 0; i < len - 1; ++i) {
            if (numbers[i] > numbers[i + 1]) {
                return numbers[i + 1];
            }
        }
        return numbers[0];
    }
};
```

## 二分查找

![](./11.png)

- mid元素 < high元素，那么mid元素在最小值的右边
- mid元素 > high元素，那么mid元素在最小值的坐标
- mid元素 = high元素，那么不能说明mid元素是最小元素，high左移动缩小区间范围

![](./11-1.png)

**复杂度分析**
时间复杂度：O(log<sub>n</sub>)。

空间复杂度: O(1)。

```cpp
class Solution {
public:
    int minArray(vector<int>& numbers) {
        int low = 0;
        int high = numbers.size() - 1;
        while (low < high) {
            int mid = low + (high - low) / 2;
            if (numbers[mid] < numbers[high]) {
                high = mid;
            } else if (numbers[mid] > numbers[high]) {
                low = mid + 1;
            } else {
                high -= 1;
            }
        }
        return numbers[low];
    }
};
```