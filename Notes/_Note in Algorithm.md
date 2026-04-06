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


### 347. 前 K 个高频元素
```
class Solution {
public:
    // priority_queue 的第三个模板参数 Compare 是一个类型（type），而非函数指针或具体对象；
    // 该类型必须能生成可调用的对象，以便在堆调整时比较元素
    // 重载 operator() 的类（即仿函数）能满足要求
    class mycomparison {
    public:
        bool operator()(const pair<int, int>& lhs, const pair<int, int>& rhs) 
        {
            return lhs.second > rhs.second;
        }
    };
    vector<int> topKFrequent(vector<int>& nums, int k) {
        std::unordered_map<int, int> map;
        for (int i = 0; i < nums.size(); i++) // 利用map进行统计
	        map[nums[i]]++;
        // priority_queue<Type, Container, Functional> 优先队列
        // Type为数据类型, Container为保存数据的容器, Functional为元素比较方式
        // Container默认为vector，Functional默认使用小于符号 < ，即大顶堆
        std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>, mycomparison> pri_que;
        // 优先队列的排序逻辑：若比较函数返回 true，表示第一个参数 (a) 应排在第二个参数 (b) 之后（即优先级更低）
        // a.second > b.second  a 的频率比 b 大，但 a 的优先级更低所以 b 作为堆顶(这里是小顶堆)

        for (auto& it : map) // 对统计数据进行排序，前k个
        {
            pri_que.push(it);
            if (pri_que.size() > k)
                pri_que.pop();
        }

        std::vector<int> result(k);
        for (int i = k - 1; i >= 0; i--) // top是频率最低的
        {
            result[i] = pri_que.top().first;
            pri_que.pop();
        }

        return result;
    }
};
```
**仿函数：**就是使一个类的使用看上去像一个函数。其实现就是类中实现一个operator()，这个类就有了类似函数的行为，就是一个仿函数类了。  
仿函数不是函数而是类；仿函数重载了()运算符，拥有函数的行为。  
在上述例子中，创建仿函数mycomparison是因为**优先级队列**的模板参数要求：  
第一个参数Type、第二个参数Container，第三个参数为Compare 。Compare是一个比较器类型而非函数指针，如果比较器返回true，则第一个参数比第二个参数优先级更低。priority_queue默认是大顶堆，也就是在堆顶的是最大的元素，大的元素优先级高，Compare默认 < 。  
对于该题应该使用小顶堆（频率前k个），所以自定义mycomparison类，使用 > ，元素更小的优先级更高，排在前面更靠近堆顶。


### 判断字符是否为数字或字母
\<cctype\>  
**isalpha：** ```int isalpha(int c);``` 若 c 是字母（a-z 或 A-Z），返回非零值；否则返回 0。  
**isdigit：** ```int isdigit(int c);``` 若 c 是数字（0-9），返回非零值；否则返回 0。  
**isalnum：** ```int isalnum(int c);``` 若 c 是字母或数字（等价于 isalpha(c) || isdigit(c)），返回非零值；否则返回 0。  


### 字母转换大小写
\<cctype>  
**tolower(char c)**  
**toupper(char c)**  
\<algorithm>  
**transform(first, last, result, op)：** first是容器的首迭代器，last为容器的末迭代器，result为存放结果的容器，op为要进行操作的一元函数对象或sturct、class。  
**transform(first1,last1,first2,result,binary_op)：** first1是第一个容器的首迭代器，last1为第一个容器的末迭代器，first2为第二个容器的首迭代器，result为存放结果的容器，binary_op为要进行操作的二元函数对象或sturct、class。