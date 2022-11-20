### [100. 相同的树](https://leetcode.cn/problems/same-tree/)
### 思路
DFS
### 代码 (cpp)
```cpp
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (p == nullptr && q == nullptr) return true;
        else if (p == nullptr || q == nullptr) return false;
        else if (p->val != q->val) return false;
        return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
    }
};
```
**复杂度分析**
- 时间复杂度：O(min(m,n)) (m, n为树的节点数)
- 空间复杂度：O(min(m,n))
