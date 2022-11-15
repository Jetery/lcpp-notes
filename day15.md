### [129. 求根节点到叶节点数字之和](https://leetcode.cn/problems/sum-root-to-leaf-numbers/)
### 思路 DFS
* 递归三部曲:
    1. 终止条件 : 已经到达叶子节点 (左右子树为空)
    2. 返回值 : 本题不用返回, 全局变量`ans`加上当前`cur`即可
    3. 本层处理问题 : 更新`cur`(cur * 10 + 左/右子树的值)
### 代码 (cpp)
```cpp
class Solution {
public:
    int ans;
    void help(TreeNode *root, int cur) {
        if (root->left == nullptr && root->right == nullptr) {
            ans += cur;
        } else {
            if (root->left != nullptr)
                help(root->left, cur * 10 + root->left->val);
            if (root->right != nullptr)
                help(root->right, cur * 10 + root->right->val);
        }

    }
    int sumNumbers(TreeNode* root) {
        if (root == nullptr) return 0;

        help(root, root->val);

        return ans;
    }
        
};
```
**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(height)
