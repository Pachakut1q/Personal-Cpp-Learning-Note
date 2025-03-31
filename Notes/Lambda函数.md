### Lambda函数
基本语法：[capture list] (parameter list) -> return type { function body }  
Lambda表达式是一种在被调用的位置或作为参数传递给函数的位置定义匿名函数对象的简便方法。
```
int Func(const std::function<int(void)>& func) //func返回类型为int，参数为void
{
	return func();
}
int main()
{	
	int a = 5;
	auto lambda = [=]() -> int { return a; }; //隐式按值捕获a，显式指定返回类型
	int b = Func(lambda);
	std::cout << b << std::endl;

	std::vector<int> values = { 1,2,3,6,9 };
	auto it = std::find_if(values.begin(), values.end(), [](int value) { return value > 3; }); 
    //省略返回值类型，由编译器根据函数体推导
    //找到values中第一个>3的值
	std::cout << *it << std::endl;

	std::cin.get();
	return 0;
}
```
console：
```
5
6
```