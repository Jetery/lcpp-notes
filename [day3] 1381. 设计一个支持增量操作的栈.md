### [1381. 设计一个支持增量操作的栈](https://leetcode.cn/problems/design-a-stack-with-increment-operation/)
### 思路
模拟题, 用 vector 模拟栈, `size` 表示当前栈大小  
需要注意的是, `increment(int k, int val)` 的 `k` 可能超过 `size`
### 代码 (cpp)
```cpp
class CustomStack {

public:
    int size = 0, max = 0;
    vector<int> stack;

    CustomStack(int maxSize) {
        max = maxSize;
    }
    
    void push(int x) {
        if (size < max) {
            stack.push_back(x);
            size++;
        }
    }
    
    int pop() {
        if (size == 0) return -1;
        size = size - 1;
        int ret = stack[size];
        stack.pop_back();
        return ret;
    }
    
    void increment(int k, int val) {
        for (int i = 0; i < size && i < k; i++) {
            stack[i] += val;
        }
    }
};
```
**复杂度分析**
- 时间复杂度：O(N)
- 空间复杂度：O(N)
