### 函数指针
```
void HelloWorld(int a)
{
	std::cout << "Hello World! Value: " << a << std::endl;
}
int main()
{
	void(*functionA)(int) = HelloWorld; // 声明一个返回值为void，参数类型为int的名为functionA的函数指针
	functionA(1);

	typedef void(*HelloWorldFunction)(int); // 创建新类型表示"指向返回void且接受int参数的函数"的指针的别名HelloWorldFunction
	HelloWorldFunction functionB = HelloWorld;
	functionB(2);

	std::cin.get();
	return 0;
}
```
```
void PrintValue(int value)
{
	std::cout << "Value: " << value << std::endl;
}
void ForEach(const std::vector<int>& values, void(*func)(int))
{
	for (int value : values)
		func(value);
}
int main()
{
	std::vector<int> values = { 1,2,3,6,9 };
	ForEach(values, PrintValue);

	std::cin.get();
	return 0;
}
```
```
void ForEach(const std::vector<int>& values, void(*func)(int))
{
	for (int value : values)
		func(value);
}
int main()
{
	std::vector<int> values = { 1,2,3,6,9 };
	ForEach(values, [](int value) {std::cout << "Value: " << value << std::endl; });//lambda函数

	std::cin.get();
	return 0;
}
```