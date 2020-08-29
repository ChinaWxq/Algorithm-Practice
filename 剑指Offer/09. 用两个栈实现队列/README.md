# 用两个栈实现队列

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

 
```
示例 1：

输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
示例 2：

输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
提示：

1 <= values <= 10000
最多会对 appendTail、deleteHead 进行 10000 次调用
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof


## 辅助栈

栈的反转就是队列。定义栈A，B

- push操作，元素放入栈A
- pop操作，如果栈B有元素，pop出，如果没有将A栈的元素全部倒入栈B，再pop元素

**复杂度分析：**

时间复杂度：O(1)。对应插入和删除都是O(1)，push时是栈的push操作，pop时看起来“执行了一次栈的倒入”，实际上每个元素只会从A pop到B一次，分摊下来是pop是O(1)的。

空间复杂度：O(n)。

空间复杂度O(n) 双栈存储。

![](./show.gif)

```cpp
class CQueue {
public:
    stack<int> stack1, stack2;
    CQueue() {
        while (!stack1.empty()) {
            stack1.pop();
        }
        while (!stack2.empty()) {
            stack2.pop();
        }
    }
    
    void appendTail(int value) {
        stack1.push(value);
    }
    
    int deleteHead() {
        if (stack2.empty()) {
            while (!stack1.empty()) {
                stack2.push(stack1.top());
                stack1.pop();
            }
        } 
        if (stack2.empty()) {
            return -1;
        } else {
            int deleteItem = stack2.top();
            stack2.pop();
            return deleteItem;
        }
    }
};

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue* obj = new CQueue();
 * obj->appendTail(value);
 * int param_2 = obj->deleteHead();
 */
```