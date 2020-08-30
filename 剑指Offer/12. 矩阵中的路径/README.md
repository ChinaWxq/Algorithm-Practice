# 矩阵中的路径

请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一格开始，每一步可以在矩阵中向左、右、上、下移动一格。如果一条路径经过了矩阵的某一格，那么该路径不能再次进入该格子。例如，在下面的3×4的矩阵中包含一条字符串“bfce”的路径（路径中的字母用加粗标出）。

[["a","b","c","e"],
["s","f","c","s"],
["a","d","e","e"]]

但矩阵中不包含字符串“abfb”的路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入这个格子。

 
```
示例 1：

输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
示例 2：

输入：board = [["a","b"],["c","d"]], word = "abcd"
输出：false
提示：

1 <= board.length <= 200
1 <= board[i].length <= 200
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof

## DFS

**复杂度分析**

时间复杂度：O(3<sup>k</sup>)

空间复杂度：O(k)

```cpp
class Solution {
public:
    vector<vector<char>> board;
    string word;
    int len, rows, cols;
    int dx[5] = {-1, 0, 1, 0, -1};
    bool exist(vector<vector<char>>& board, string word) {
        this->board = board;
        this->word = word;
        this->len = word.size();
        this->rows = board.size();
        this->cols = board[0].size();
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < cols; ++j) {
                if (dfs(i, j, 0)) {
                    return true;
                }
            }
        }
        return false;
    }

    bool dfs(int i, int j, int pos) {
        // 下标是否满足条件 
        if (i < 0 || i >= rows || j < 0 || j >= cols) {
            return false;
        }
        // 是否被访问，是否满足当前匹配条件
        if (board[i][j] == '#' || board[i][j] != word[pos]) {
            return false;
        }
        // 是否满足返回条件
        if (pos + 1 == len) {
            return true;
        }
        // 标记
        char tmp = board[i][j];
        board[i][j] = '#';
        // dfs
        for (int k = 0; k < 4; ++k) {
            if (dfs(i + dx[k], j + dx[k+1], pos+1)) {
                return true;
            }
        }
        // 回溯
        board[i][j] = tmp;
        return false;
    }
};
```