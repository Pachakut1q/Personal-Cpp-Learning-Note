### 虚析构函数
```
class Base
{
public:
	Base() { std::cout << "Base Constructor\n"; }
	~Base() { std::cout << "Base Destructor\n"; }
};
class Derived : public Base
{
public:
	Derived() { std::cout << "Derived Constructor\n"; }
	~Derived() { std::cout << "Derived Destructor\n"; }
};

int main()
{
	Base* base = new Base();
	delete base;
	std::cout << "-------------\n";
	Derived* derived = new Derived();
	delete derived;
	std::cout << "-------------\n";
	Base* poly = new Derived();
	delete poly;
	std::cin.get();
	return 0;
}
```
result：
```
Base Constructor
Base Destructor
-------------
Base Constructor
Derived Constructor
Derived Destructor
Base Destructor
-------------
Base Constructor
Derived Constructor
Base Destructor
```
poly被delete时只调用了基类的析构函数而没有调用派生类的析构函数。这会造成内存泄漏。  
为什么？poly 的静态类型是 Base*，编译器在编译时根据指针类型决定调用哪个析构函数。由于 Base 的析构函数 不是虚函数，编译器直接调用 Base::~Base()，而不会查找派生类的析构函数。  
解决方法：虚析构函数，在基类析构函数前面加上virtual关键字。但是与普通的虚函数不同，虚析构函数的意思不是覆写（override），而是加上一个析构函数，它会让编译器去查找派生类的析构函数并调用。
```
virtual ~Base() { std::cout << "Base Destructor\n"; }
```
