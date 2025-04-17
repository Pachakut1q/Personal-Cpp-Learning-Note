### this
this是一个指向当前对象实例的 指针 。
```
void PrintEntity(const Entity& e);

class Entity
{
public:
	int x, y;

	Entity(int x, int y)
	{
		this->x = x; // or (*this).x = x;
		this->y = y; // or (*this).y = y;

		PrintEntity(*this);
	}

};
void PrintEntity(const Entity& e)
{
	//do something
}
```
### static
两种用法：  
1、在类或结构体外部使用static关键字  
2、在类或结构体内部使用static  

1、外部  
如果在项目中创建一个static.cpp
```
//static.cpp
static int s_Variable = 5;
//这个变量只会在这个翻译单元内部链接，有点像private私有属性
```
```
//main.cpp
int s_Variable = 10;
//和static.cpp中的变量互不干扰
//但是如果去掉static，就会出现重复定义错误（link阶段）
//此时可以加上extern关键字（在外部翻译单元中寻找该变量）
//extern int s_Variable = 10;
```
总结一下，当在类或结构体外部声明静态函数或静态变量时，其只会在声明的Cpp文件中链接；最好让函数和变量标记为静态，除非真的需要它们跨翻译单元链接。  
  
2、内部  
如果在一个类中定义了一个静态变量，那么在类的所有实例中，这个变量只有一个实例。  
静态方法无法访问非静态变量，因为静态方法没有类实例。

(3、Local Static  
```
class Singleton
{
public:
  static Singleton& Get()//初始化，&引用
  {
    static Singleton instance;//通过static，构造一个单例实例，其生命周期被延长至程序结束
    return instance;
  }
  void Hello() {}
}
int main()
{
  Singleton::Get().Hello();//访问单例实例
  return 0;
}
```
)
### const
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
### mutable
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
### 关键字new
```
int* a = new int;
int* b = new int[10];
Entity* e = new Entity();//相当于Entity* e = (Entity*)malloc(sizeof(Entity)),但是最大的区别在于new调用了Entity的构造函数
Entity* e1 = new Entity[10];

delete a;
delete[] b;
delete e;
delete[] e1;//不要忘了delete
```