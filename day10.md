### [160. 相交链表](https://leetcode.cn/problems/intersection-of-two-linked-lists/)
### 思路 双指针
每次移动步长为 1, 只要当一条链表走到尾就从另一条的链表头开始走  
如此, 两指针行走的路程相同, 在速度相同的情况下, 两指针一定会相遇
### 代码 (cpp)
```cpp
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if (!headA || !headB) return nullptr;
        ListNode *a = headA, *b = headB;
        while (a != b) {
            a = a == nullptr ? headB : a->next;
            b = b == nullptr ? headA : b->next;
        }
        return a;
    }
};
```
**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(1)
