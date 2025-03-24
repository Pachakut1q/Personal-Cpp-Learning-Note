### auto
auto关键字用于自动类型推断，允许编译器根据初始化表达式推导变量的类型。
```
auto i = 42;
auto str = "hello";
auto vec = std::vector<int>{1, 2, 3};
```
在处理迭代器、模板或长类型名时，auto能显著减少代码冗余
```
// 传统写法
std::vector<int>::iterator it = vec.begin();

// 使用 auto
auto it = vec.begin(); // 编译器自动推导为 vector<int>::iterator
```