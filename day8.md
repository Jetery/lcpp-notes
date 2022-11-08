### [24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/)
### 思路 1: 迭代
#### 添加傀儡节点`dummy`后不用考虑边界问题
* 两两反转节点需要四个指针在手里
  1. a : 局部头节点 (用于连接反转后的头)
  2. b : 反转的第一个节点
  3. c : 反转的第二个节点
  4. d : 局部尾节点 (被反转后的尾连接)
* 步骤 :
  1. a 指向 c ( c 为反转后的头) 
  2. c 指向 b (反转)
  3. b 指向 d ( b 为反转后的尾)
  4. 更新 a 为 b ( 下一步的局部头节点) ; 更新 b 为 `a->next`
### 代码 (cpp)
```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummy = new ListNode(-1);
        dummy->next = head;
        ListNode *a = dummy, *b = head;
        while (b != nullptr && b->next != nullptr) {
            ListNode* c = b->next;
            ListNode* d = c->next;
            a->next = c;
            c->next = b;
            b->next = d;
            a = b;
            b = a->next;
        }

        return dummy->next;
    }
};
```
**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(1)
-----
### 思路 2: 递归
* 递归三部曲:
  1. 终止条件 : 当前节点或下一节点为空
  2. 返回值 : 反转后的部分头节点
  3. 本层处理问题 : 两两反转节点
### 代码 (cpp)
```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if (head == nullptr || head->next == nullptr) {
            return head;
        }

        ListNode* next = head->next;
        head->next = swapPairs(next->next);
        next->next = head;
        
        return next;
    }
};
```
**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(1)