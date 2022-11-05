### [232. 用栈实现队列](https://leetcode.cn/problems/implement-queue-using-stacks/submissions/)
### 思路
使用两个栈模拟队列
### 代码 (cpp)
```cpp
class MyQueue {
public:
    stack<int> input;
    stack<int> output;
    MyQueue() {

    }
    
    void push(int x) {
        input.push(x);
    }
    
    int pop() {
        int ret = 0;
        if (output.size() > 0) {
            ret = output.top();
            output.pop();
        } else {
            while (!input.empty()) {
                output.push(input.top());
                input.pop();
            }
            ret = output.top();
            output.pop();
        }
        return ret;
    }
    
    int peek() {
        int ret = 0;
        if (output.size() > 0) {
            ret = output.top();
        } else {
            while (!input.empty()) {
                output.push(input.top());
                input.pop();
            }
            ret = output.top();
        }
        return ret;
    }
    
    bool empty() {
        return input.empty() && output.empty();
    }
};
```
**复杂度分析**
- 时间复杂度：O(N)
- 空间复杂度：O(N)
