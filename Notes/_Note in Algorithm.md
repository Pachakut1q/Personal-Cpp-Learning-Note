### 49.字母异位词分组
```
vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> map;
        for (string& str : strs)
        {
            string key = str;
            sort(key.begin(), key.end());
            map[key].emplace_back(str);
        }
        vector<vector<string>> result;
        for (auto it = map.begin(); it != map.end(); it++)
        {
            result.emplace_back(it->second);
        }
        return result;
    }
```
for (string& str : strs)  
使用 & 零复制开销  
for (auto it = map.begin(); it != map.end(); it++)  
it++ 将迭代器移动到下一个元素，直到覆盖整个容器。迭代器抽象了底层存储的复杂性。无论元素是否连续，it++ 都能正确跳到下一个有效元素。