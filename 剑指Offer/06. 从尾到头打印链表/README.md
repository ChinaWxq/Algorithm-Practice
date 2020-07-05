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

### vector辅助存储

利用vector a记录遍历链表的元素，然后反向赋值给vector b。

时间复杂度：O(n)

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
        vector<int> a, b;
        ListNode *tmp = head;
        while (tmp != NULL) {
            a.push_back(tmp->val);
            tmp = tmp->next;
        }
        for (int i = a.size() - 1; i >= 0; --i) {
            b.push_back(a[i]);
        }
        return b;
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
    vector<int> a;
    vector<int> reversePrint(ListNode* head) {
        ListNode *pre = NULL;
        ListNode *cur = head;
        ListNode *next = NULL;
        while (cur) {
            next = cur->next;
            cur->next = pre;
            pre = cur;
            cur = next;
        }
        while (pre) {
            a.push_back(pre->val);
            pre = pre->next;
        }
        return a;
    }
};
```
时间复杂度：O(n)