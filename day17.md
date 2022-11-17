### [297. 二叉树的序列化与反序列化](https://leetcode.cn/problems/serialize-and-deserialize-binary-tree/)
### 思路 DFS
* 序列化: 通过前序遍历构造字符串  
    - 节点为空, 追加 `"null,"`
    - 节点不为空, 追加 `to_string(root->val) + ","` // (`","`别忘)  
* 反序列化: 由于序列化是前序遍历, 反序列化也要前序遍历  
通过`stringstream`来过滤序列化的分隔符, 使用队列`queue`来存取值  
#### 本次增长的知识:
- 熟悉cpp中`stringstream`的使用
- 字符串和整型之间的转化通过方法`to_string()`和`stoi()`
### 代码 (cpp)
```cpp
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        if (!root) return "#_";
        string ans = to_string(root->val) + "_";
        ans += serialize(root->left);
        ans += serialize(root->right);
        return ans;
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        stringstream ss(data);
        string cur;
        queue<string> queue;
        while (getline(ss, cur, '_')) 
            queue.push(cur);
        
        return preOrd(queue);
    }

    TreeNode* preOrd(queue<string> &q) {
        string val = q.front();
        q.pop();
        if (val == "#") return NULL;
        auto root = new TreeNode(stoi(val));
        root->left = preOrd(q);
        root->right = preOrd(q);
        return root;
    }
};
```
**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(n)
