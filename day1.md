### [989. 数组形式的整数加法](https://leetcode-cn.com/problems/add-to-array-form-of-integer/)
### 思路
模拟竖式的加法, 得到每个数组的最低位, 从最低位开始加\
注意 _循环结束后_ 对进位 `t` 的判断
### 代码 (cpp)
```cpp
class Solution {
public:
    vector<int> addToArrayForm(vector<int>& num, int k) {
        vector<int> a, b;
        for (int i = num.size() - 1; i >= 0; i--) a.push_back(num[i]);
        while (k != 0) {
            b.push_back(k % 10);
            k /= 10;
        }
        vector<int> temp;
        int t = 0;
        for (int i = 0; i < a.size() || i < b.size(); i++) {
            if (i < a.size()) t += a[i];
            if (i < b.size()) t += b[i];
            temp.push_back(t % 10);
            t /= 10;
        }
        if (t) temp.push_back(1);
        vector<int> ans;
        for (int i = temp.size() - 1; i >= 0; i--) ans.push_back(temp[i]);
        return ans;
    }
};
```
**复杂度分析**
- 时间复杂度：O(N)
- 空间复杂度：O(N)
