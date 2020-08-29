# 替换空格

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

 

**示例 1：**

`
输入：s = "We are happy."
输出："We%20are%20happy."
` 

**限制：**

`
0 <= s 的长度 <= 10000
`

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof


## 解法

### 暴力搜索

用一个临时字符串变量存储，搜索目标字符串
规定目标字符串为a，临时字符串为b
- 如果a[i]是空格，那么b追加`%20`字符串
- 如果a[i]不是空格，那么b追加'%20'

**复杂度分析**

时间复杂度：O(n)
空间复杂度：O(n)


```cpp
class Solution {
public:
    string replaceSpace(string s) {
        string str;
        for (int i = 0; i < s.size(); ++i) {
            if (s[i] != ' ') {
                str += s[i];
            } else {
                str += "%20";
            }
        }
        s = str;
        return s;
    }
};
```