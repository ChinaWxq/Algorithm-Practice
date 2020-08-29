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

1. 前序序列第一个结点是二叉树的根结点。
2. 根据根结点在中序序列中的位置，前部分为根结点的左子树，后部分为根结点的右子树。
3. 再对分割出来的左子树和右子树进行递归分析。

**复杂度分析**

时间复杂度：O(n)。对于每个结点都有创建过程以及左右子树重建的过程。

空间复杂度：O(n)。存储整棵树的开销。

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

    TreeNode* rebuild(vector<int>& preorder, int pre_root, int in_left, int in_right) {
        if (in_left > in_right) {
            return NULL;
        }
        TreeNode *root = new TreeNode(preorder[pre_root]);
        int idx = m[root->val];
        root->left = rebuild(preorder, pre_root+1, in_left, idx-1);
        // 左子树在前序遍历的边界就是右子树的开始
        root->right = rebuild(preorder, pre_root+idx-in_left+1, idx+1, in_right);
        return root;
    }
};
```