### [1. 两数之和](https://leetcode.cn/problems/two-sum/)
### 思路
hash表, 键值对中键为`nums[i]`, 值为`i`, 如果`target - nums[i]`存在就返回 
### 代码 (cpp)
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> mp;
        for (int i = 0; i < nums.size(); i++) {
            auto iter = mp.find(target - nums[i]);
            if (iter != mp.end()) {
                return {iter->second, i};
            }
            mp[nums[i]] = i;
        }
        return {};
    }
};
```
**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(n)
