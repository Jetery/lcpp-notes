### [109. 有序链表转换二叉搜索树](https://leetcode.cn/problems/convert-sorted-list-to-binary-search-tree/)
### 思路 双指针
由于链表有序, 只要找到了中间节点, 就得到了二叉搜索树的根节点, 如此再递归处理左右的链表  
* 递归三部曲:
    1. 终止条件 : 当前节点或下一节点为空
    2. 返回值 : 构造出的树的根节点
    3. 本层处理问题 : 找到当前要处理的链表的中间节点, 链表左边为树的左分支, 右边为右分支  

**注意事项 :** 一定要记得将找到的中间节点和原链表断开
### 代码 (cpp)
```cpp
class Solution {
public:
    TreeNode* sortedListToBST(ListNode* head) {
        TreeNode *root;
        if (head == nullptr) return nullptr;
        else if (head->next == nullptr) {
            root = new TreeNode(head->val);
            return root;
        }

        ListNode *fast = head, *slow = head, *pre = head;
        // 让 slow 指向中间节点
        while (fast != nullptr && fast->next != nullptr) {
            fast = fast->next->next;
            slow = slow->next;
        }

        while (pre->next != slow) pre = pre->next;
        root = new TreeNode(slow->val);
        pre->next = nullptr; // 从中间断开链表, 防止递归时链表长度不变
        // 递归处理
        root->left = sortedListToBST(head);
        root->right = sortedListToBST(slow->next);

        return root;

    }
};
```
**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(logn)
