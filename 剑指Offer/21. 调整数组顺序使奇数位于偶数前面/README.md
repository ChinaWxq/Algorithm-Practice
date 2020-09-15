# 调整数组顺序使奇数位于偶数前面

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。

```cpp
示例：

输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。
 

提示：

1 <= nums.length <= 50000
1 <= nums[i] <= 10000
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof

## 直接法

复杂度分析：

时间复杂度：O(n)。
空间复杂度：O(n)。

```cpp
class Solution {
public:
    vector<int> exchange(vector<int>& nums) {
        vector<int> a;
        vector<int> b;
        for (int i = 0; i < nums.size(); ++i) {
            if (nums[i] & 1) {
                a.push_back(nums[i]);
            } else {
                b.push_back(nums[i]);
            }
        }
        for (int i = 0; i < b.size(); ++i) {
            a.push_back(b[i]);
        }
        return a;
    }
};
```

## 首尾指针

low指针搜索偶数的位置，high指针搜索奇数的位置，然后交换奇偶数位置。

复杂度分析：

时间复杂度：O(n)。

空间复杂度：O(1)。

```cpp
class Solution {
public:
    vector<int> exchange(vector<int>& nums) {
        int low = 0, high = nums.size() - 1;
        while (low < high) {
            if (nums[low] & 1) {
                low++;
                continue;
            }
            if ((nums[high] & 1) == 0) {
                high--;
                continue;
            }
            swap(nums[low++], nums[high--]);
        }
        return nums;
    }
};
```