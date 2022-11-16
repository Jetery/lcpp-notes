### [513. 找树左下角的值](https://leetcode.cn/problems/find-bottom-left-tree-value/)
### 思路
层序遍历, 返回最后一层的第一个元素即可
### 代码 (cpp)
```cpp
class Solution {
public:
    int findBottomLeftValue(TreeNode* root) {
        queue<TreeNode*> queue;
        vector<int> list;
        queue.push(root);
        while (!queue.empty()) {
            list.clear();
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                auto cur = queue.front();
                queue.pop();
                list.push_back(cur->val);
                if (cur->left) queue.push(cur->left);
                if (cur->right) queue.push(cur->right);
            }
        }
        return list[0];
    }
};
```
**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(n)
