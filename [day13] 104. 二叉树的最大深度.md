### [104. 二叉树的最大深度](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)
### 思路
DFS
### 代码 (cpp)
```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr) return 0;
        return 1 + max(maxDepth(root->left), maxDepth(root->right));
    }
};
```
**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(height)
 