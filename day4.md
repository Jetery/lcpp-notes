### [394. 字符串解码](https://leetcode.cn/problems/decode-string/)
### 思路 1: 双栈
* 使用 `num` 栈记录重复次数 ; `str` 栈记录要重复的字符 ; 
* `n` 为当前数字, `ans` 为解码后的字符
  - 当 `c >= '0' && c <= '9'` 时 , 更新数字 `n`
  - 当 `c == 'a' && c <= 'z'` 时, 更新 `ans`
  - 当 `c == '['` 时, 为了保留当前信息, 处理`[`后信息, 故将 `num` 压入当前数字, `n` 置为 0 ; `str` 压入当前字符, `ans = ""`
  - 当 `c == ']'` 时, `ans` 已经为最近的`[`和当前`]`内的字符, 得到重复次数 `t = num.top()`, 
  将当前字符按照 `t` 添加到外层字符 `str.top()` 后, 完成了部分解码, 更新 `ans`, 将栈内元素弹出
  
### 代码 (cpp)
```cpp
class Solution {
public:
    string decodeString(string s) {
        stack<int> num;
        int n = 0;
        stack<string> str;
        string ans = "";
        for (char c : s) {
            if (c >= '0' && c <= '9') {
                n = n * 10 + c - '0';
            } else if (c == '[') {
                num.push(n);
                n = 0;
                str.push(ans);
                ans = "";
            } else if (c == ']') {
                int t = num.top();
                num.pop();
                for (int i = 0; i < t; i++) {
                    str.top() += ans;
                }
                ans = str.top();
                str.pop();
            } else {
                ans += c;
            }
        }
        return ans;
    }

};
```
**复杂度分析**
- 时间复杂度：O(N)
- 空间复杂度：O(N)

---

### 思路 2: 栈 + 递归

* 仅遇到`[`和`]`时和思路 1 不同  
    - 当 `c == '['` 时, 递归处理后续字符, 得到返回值 `sub`, 按次数添加`sub`, `n`置为0
    - 当 `c == ']'` 时, 说明此级别的 `'[]'`内字符已处理完

### 代码 (cpp)
```cpp
class Solution {
public:
    string helper(stack<char> &stack) {
        int n = 0;
        string ret = "";
        while (!stack.empty()) {
            char c = stack.top();
            stack.pop();
            if (c >= '0' && c <= '9') {
                n = n * 10 + c - '0';
            } else if (c == '[') {
                string sub = helper(stack);
                for (int i = 0; i < n; i++) {
                    ret += sub;
                }
                n = 0;
            } else if (c == ']'){
                break;
            } else {
                ret += c;
            }
        }
        return ret;
    }
    
    string decodeString(string s) {
        stack<char> stack;
        for (int i = s.size() - 1; i >= 0; i--)
            stack.push(s[i]);
        string ret = helper(stack);
        return ret;
    }
};
```
**复杂度分析**
- 时间复杂度：O(N)
- 空间复杂度：O(N)