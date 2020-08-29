# 从头到尾打印链表

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

 

**示例 1：**

`
输入：head = [1,3,2]
输出：[2,3,1]
`

**限制：**

`
0 <= 链表长度 <= 10000
`

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof

## 解法

### vector反转

利用vector记录遍历链表的元素，然后反转vector。

**复杂度分析**

时间复杂度：O(n)。

空间复杂度：O(n)。

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        vector<int> v;
        ListNode *p = head;
        while (p != NULL) {
            v.push_back(p->val);
            p = p->next;
        }
        reverse(v.begin(), v.end());
        return v;
    }
};
```

### 反转链表

设置两个辅助指针将原链表反转存入vector。
cur为当前结点指针，next为下一个结点指针，pre为上一个结点指针


```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        vector<int> ans;
        ListNode *pre = NULL, *cur = head, *next = NULL;
        while (cur != NULL) {
            next = cur->next;
            cur->next = pre;
            pre = cur;
            cur = next;
        }
        while (pre != NULL) {
            ans.push_back(pre->val);
            pre = pre->next;
        }
        return ans;
    }
};
```

**复杂度分析**

时间复杂度：O(n)。

空间复杂度：O(n)。