### 函数指针
```
void HelloWorld(int a)
{
	std::cout << "Hello World! Value: " << a << std::endl;
}
int main()
{
	void(*functionA)(int) = HelloWorld;
	functionA(1);

	typedef void(*HelloWorldFunction)(int);
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