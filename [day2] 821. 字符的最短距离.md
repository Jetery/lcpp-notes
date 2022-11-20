### [821. 字符的最短距离](https://leetcode.cn/problems/shortest-distance-to-a-character/)
### 思路 1 两次遍历

* 第一次遍历记录满足条件字符下标 `k` : 
  1.  满足条件, 更新左边界 `k`
  2.  不满足条件 , 直接填入 `k` (左边满足条件的下标 or 左边不存在满足的下标)  

  此时 `k` 停留在最后一个满足条件的位置 (题目数据保证 `c` 在 `s` 中至少出现一次)

* 第二次遍历时记录右边满足条件的下标 :
  1. 满足条件, 更新右边界 `k`
  2. 不满足条件, 填入 ___当前下标 `i` 和左边界的距离 `i - ans[i]`___  和  ___右边界 `k` 的距离 `i - k`___ 的最小值
    - 当 `k` 被更新后, `i`继续向左移动 , 会造成 `i - k` 为负值, 所以需要加上绝对值
    - 若使用 `k - i` , 当 `k` 没有停留在 `s.size() - 1` , 依旧有可能 `k - i < 0`, 故仍需要绝对值
### 代码 (cpp)
```cpp
class Solution {
public:
    vector<int> shortestToChar(string s, char c) {
        int n = s.size();
        vector<int> ans(n, -1);
        int k = -n;
        // get the left distance
        for (int i = 0; i < n; i++) {
            if (s[i] == c) k = i;
            ans[i] = k;
        }
        // get the right distance then compare with left distance 
        for (int i = n - 1; i >= 0; i--) {
            if (s[i] == c) k = i;
            ans[i] = min(i - ans[i], abs(i - k));
        }

        return ans;
    }
};
```
**复杂度分析**
- 时间复杂度：O(2N) -> O(N)
- 空间复杂度：O(N)

-------

### 思路 2 一次遍历

* 对思路 1 的优化
  - `l` 为左边界 , `r` 为右边界
  - `i` 从头遍历数组 , `j` 从尾遍历数组
  - 遇到满足条件的情况分别更新 `l` , `r` 
  - 若 `i >= l` 说明当前下标左边有符合条件的 `c` ; 同理 , `j <= r` 则右边有
  - 取最小值min
  - 由于 `i` , `j` 指针相遇后仍继续移动 , 可以做到不遗漏


### 代码 (cpp)
```cpp
class Solution {
public:
    vector<int> shortestToChar(string s, char c) {
        vector<int> ans(s.size(), INT_MAX);
        int l = s.size(), r = -1, n = s.size();
        for (int i = 0; i < s.size(); i++) {
            int j = n - 1 - i;
            if (s[i] == c) l = i;
            if (s[j] == c) r = j;
            if (i >= l) ans[i] = min(ans[i], i - l);
            if (j <= r) ans[j] = min(ans[j], r - j);
        }
        return ans;
    }
};
```
**复杂度分析**
- 时间复杂度：O(N)
- 空间复杂度：O(N)