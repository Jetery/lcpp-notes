### [142. 环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/)
### 思路 快慢指针
令快指针`fast`步长为2, 慢指针`slow`步长为1  
假设链表有环, 记链表头到开始入环的第一个节点之前的节点路程为`x`, 整个环路长度为`cycle`, 快慢指针相遇点 到 入环的第一个节点的路程为`y`  
由于`fast`速度是`slow`两倍, 就有式子`2 * (x + cycle -y) = x + n * cycle - y`  
化简得`x = (n - 2) * cycle + y` 由于`cycle`是环路长度, 可以忽略, 得到`x = y`  
即相遇后慢指针`slow`从头出发, 快指针`fast`在相遇点出发, 步长都为1, 会再次在入环点相遇
### 代码 (cpp)
```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode *slow = head, *fast = head;
        while (fast != nullptr && fast->next != nullptr) {
            fast = fast->next->next;
            slow = slow->next;
            if (fast == slow) break;
        }

        if (fast == nullptr || fast->next == nullptr) return nullptr;
        slow = head;
        while (slow != fast) {
            slow = slow->next;
            fast = fast->next;
        }
        return slow;
    }
};
```
**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(1)
