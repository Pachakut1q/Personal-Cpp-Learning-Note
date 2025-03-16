### 关键字Const
```
const int MAX_SIZE = 100; // 全局常量（静态存储区）
void func() {
    const int local = 5;  // 栈区常量，每次函数调用重新初始化
}

const int* ptr1;        // 指向常量数据（数据不可改）
int* const ptr2;        // 常量指针（指针不可改）
const int& ref = x;     // 常量引用（不可通过ref修改x）

class MyClass {
    void readOnlyFunc() const; // 承诺不修改成员变量
};
const MyClass obj;
obj.readOnlyFunc(); // 合法调用
```
