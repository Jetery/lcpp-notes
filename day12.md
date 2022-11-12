### [146. LRU 缓存](https://leetcode.cn/problems/lru-cache/description/)
### 思路
用`list`来维护关键字的新旧, `map`来记录关键字的键值对  
#### 小技巧: 由于put时也会对元素新旧产生影响, 可以在put时调用get
### 代码 (Java)  
```java
class LRUCache {

    private HashMap<Integer, Integer> map;
    private ArrayList<Integer> list;
    private int max;

    public LRUCache(int capacity) {
        max = capacity;
        map = new HashMap<>();
        list = new ArrayList<>();
    }
    
    public int get(int key) {
        if (map.containsKey(key)) {
            for (int i = 0; i < list.size(); i++) {
                if (list.get(i) == key) {
                    list.remove(i);
                    list.add(key);
                    break;
                }
            }
            return map.get(key);
        }
        else return -1;
    }
    
    public void put(int key, int value) {
        if (this.get(key) == -1) {
            if (list.size() == max) {
                int rm = list.get(0);
                list.remove(0);
                map.remove(rm);
            }
            list.add(key);
        }
        
        map.put(key, value);
    }
}
```
**复杂度分析**
- 时间复杂度：O(1)
- 空间复杂度：O(n)
