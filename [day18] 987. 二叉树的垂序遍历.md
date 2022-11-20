### [987. 二叉树的垂序遍历](https://leetcode.cn/problems/vertical-order-traversal-of-a-binary-tree/)
### 思路 
DFS
#### 本次增长的知识:  
`multiset`的使用, `pair`的使用
### 代码 (cpp)
```cpp
class Solution {
public:
    typedef map<int, multiset<pair<int, int>>> MAP;

    void dfs(TreeNode* root, int x, int y, MAP &mp) {
        if (!root) return ;
        mp[y].insert({x, root->val});
        dfs(root->left, x + 1, y - 1, mp);
        dfs(root->right, x + 1, y + 1, mp);
    }

    vector<vector<int>> verticalTraversal(TreeNode* root) {
        MAP mp;
        dfs(root, 0, 0, mp);
        vector<vector<int>> ans;
        for (auto &[a, b] : mp) {
            vector<int> temp;
            for (auto &e : b) {
                temp.push_back(e.second);
            }
            ans.push_back(temp);
        }
        return ans;
    }
};
```
**复杂度分析**
- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)
