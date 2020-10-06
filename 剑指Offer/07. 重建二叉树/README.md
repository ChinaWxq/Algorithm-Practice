# 重建二叉树

输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

 
**例如，给出**

```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
返回如下的二叉树：

    3
   / \
  9  20
    /  \
   15   7
```

**限制：**

`0 <= 节点个数 <= 5000`

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof

## 解法

### 递归

算法背景：

前序遍历：VLR 先访问根结点N，再遍历左子树L，再遍历右子树R。根左右。

中序遍历：LDR 先访问左子树L，再访问根结点，再遍历右子树R。左根右。

根据前序遍历和中序遍历可以确定二叉树：

1. 前序遍历首个元素是根结点root的值。
2. 根据根结点在中序遍历中的位置，前部分为根结点的左子树，后部分为根结点的右子树。
3. 根据中序遍历中左右子树的结点数量，将前序遍历分为左右子树。
4. 递归分析左右子树。

**复杂度分析**

时间复杂度：O(n)。n为结点数量。初始化哈希map需要遍历inorder，占用O(n)；递归建立n个结点，递归占用O(n)（最差情况下所有子树只有左结点，树退化为链表，递归深度为O(n)，平均情况下递归深度为O(log<sub>2</sub>n)）。

空间复杂度：O(n)。哈希map使用O(n)空间，递归使用系统O(n)空间。

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    map<int, int> m; // 存储中序遍历元素对应的位置，优化根结点在中序遍历中的搜索过程。
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        for (int i = 0; i < inorder.size(); ++i) {
            m[inorder[i]] = i;
        }
        return rebuild(preorder, 0, 0, inorder.size() - 1);
    }
    /*
        @param pre_root 前序遍历子树的根索引
        @param in_left 中序遍历左边界 
        @param in_right 中序遍历右边界
    */
    TreeNode* rebuild(vector<int>& preorder, int pre_root, int in_left, int in_right) {
        if (in_left > in_right) {
            return NULL;
        }
        TreeNode *root = new TreeNode(preorder[pre_root]);
        int idx = m[root->val];
        // 左子树的根结点索引在前序遍历中的位置是，根结点索引下一个位置。
        // 中序遍历的左边界in_left，右边界是idx-1。
        root->left = rebuild(preorder, pre_root+1, in_left, idx-1);
        // 右子树的根结点索引在前序遍历中的位置是，根结点索引+左子树数量+1。左子树数量为idx - in_left
        // 中序遍历左边界idx+1，右边界in_right。
        root->right = rebuild(preorder, pre_root+idx-in_left+1, idx+1, in_right);
        return root;
    }
};
```