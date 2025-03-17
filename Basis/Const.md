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
### 关键字Mutable
将数据成员设置为可变的，就可以在const函数中对mutable变量进行修改。一般与const配合使用，有时也用于lambda表达式中。
```
class Entity
{
private:
  string m_Name;
  mutable int m_DebugCount;
public:
  const string& GetName() const
  {
    m_DebugCount++;
    return m_Name;
  }
};

int main()
{
  const Entity e;
  e.GetName();

  cin.get();
  return 0;
}
```

