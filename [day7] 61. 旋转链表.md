### [61. 旋转链表](https://leetcode.cn/problems/rotate-list/)
### 思路
* 遍历两次
  - 第一次遍历得到链表长度`size`并构成环形链表
  - 第二次得到`size - k - 1`个结点, 在此处将链表断开即可
### 代码 (cpp)
```cpp
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        if (k == 0 || head == NULL || head->next == NULL) {
            return head;
        }
        
        int size = 1;
        ListNode* cur = head;
        while (cur->next != NULL) {
            cur = cur->next;
            size++;
        }
        cur->next = head;

        k %= size;
        for (int i = size - k - 1; i > 0; i--) {
            head = head->next;
        }

        cur = head->next;
        head->next = NULL;

        return cur;
    }
};
```
**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(1)
