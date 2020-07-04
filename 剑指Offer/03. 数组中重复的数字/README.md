# 数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

**示例 1：**

`
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
`

**限制：**

`2 <= n <= 100000`

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof

## 解法

### 解法一：记忆存储法

**思路**
根据题意数组中某些数字是重复的，找出重复的数字。数组的长度为n，且数字在0~n-1范围内，n的最大值1e5。那么很容易想到用一个全局数组，才存储每个数组元素来记录出现的次数。
我们定义：a[i]，表示元素i出现的次数。由于元素i的最大值1e5，所以不会导致全局数组过大导致的栈溢出。


```cpp
const int MAXN = 1e5 + 10;
class Solution {
public:
    int a[MAXN];
    int findRepeatNumber(vector<int>& nums) {
        int len = nums.size();
        for (int i = 0; i < len; ++i) {
            a[nums[i]]++;// 将数组元素i存储起来
            if (a[nums[i]] >= 2) { // 如果出现次数为2那么即可返回
                return nums[i];
            }
        }
        return -1;
    }
};
```
**复杂度分析**
时间复杂度：O(n)，一次循环遍历。
空间复杂度：O(n)，开辟了一个全局数组辅助。

### 解法二：原地置换

题目长度为n的数组中存放0~n-1范围的元素，如果没有重复的元素，那么可以使下标对应元素使得`nums[i] == i`

1. 遍历数组nums，设初始索引为`i = 0`
2. 若`nums[i] == i`，则对应元素在索引位置无需交换，i++
3. 若`nums[nums[i]] == nums[i]`，说明索引`nums[i]`处的元素为`nums[i]`，找到重复值，返回`nums[i]`
4. 否则交换索引i和nums[i]的元素值

```cpp
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int len = nums.size();
        int i = 0;
        while (i < len) {
            if (nums[i] == i) {
                i++;
            } else if (nums[i] == nums[nums[i]]) {
                return nums[i];
            } else {
                nums[nums[i]] = nums[i];
            }
        }
        return -1;
    }
};
```