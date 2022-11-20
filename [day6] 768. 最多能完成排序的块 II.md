### [768. 最多能完成排序的块 II](https://leetcode.cn/problems/max-chunks-to-make-sorted-ii/)
### 思路 1: 排序 + 哈希表
先将原数组复制且排序得到`clone`, 比较`arr`和`clone`, 如果在`[0,i]`范围内, 出现的数字频率一致, 那么就有1种分法
* 使用哈希表对`arr[i]`进行计数:   
    - 处理`arr[i]`时, 对`map[arr[i]]`进行计数加一
    - 处理`clone[i]`时, 对`map[clone[i]]`进行计数减一
    - __注意 :__ 只有变为 0 或者 1 / -1 时候才去操作, 这样才能真正按照不同数字来拆分，而不和数字本身数量有关
### 代码 (cpp)
```cpp
class Solution {
public:
    int maxChunksToSorted(vector<int>& arr) {
        // 已经排序的数组
        vector<int> clone = arr;
        sort(clone.begin(), clone.end());
        
        int ans = 0, window = 0;
        // 使用哈希表进行计数
        unordered_map<int, int> map;

        for (int i = 0; i < arr.size(); i++) {
            map[arr[i]]++;
            if (map[arr[i]] == 0) window--;
            else if (map[arr[i]] == 1) window++;

            map[clone[i]]--;
            if (map[clone[i]] == 0) window--;
            else if (map[clone[i]] == -1) window++;

            if (window == 0) ans++;
        }

        return ans;
    }
};
```
**复杂度分析**
- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)
---
### 思路 2: 单调栈
递增的数列才可以分割, 更小的元素要放在前方, 已经构成单调栈性质  
### 代码 (cpp)
```cpp
class Solution {
public:
    int maxChunksToSorted(vector<int>& arr) {
        stack<int> stack;
        for (int elem : arr) {
            if (stack.empty() || stack.top() <= elem) stack.push(elem);
            else {
                int curMax = stack.top(); stack.pop();
                while (!stack.empty() && stack.top() > elem) stack.pop();
                stack.push(curMax);
            }
        }
        return stack.size();
    }
};
```
**复杂度分析**
- 时间复杂度：O(N)
- 空间复杂度：O(N)