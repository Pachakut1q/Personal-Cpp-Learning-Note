### 排序
```
#include <iostream>
#include <vector>
#include <algorithm>
int main()
{
	std::vector<int> vec = { 3,5,1,4,2 };
	std::sort(vec.begin(), vec.end());
	for (int value : vec)
		std::cout << value << std::endl;
	std::cin.get();
	return 0;
}
```
std::sort()默认按照升序排列，如果使用比较函数，  
比如std::greater模板函数：
```
#include <iostream>
#include <vector>
#include <algorithm>
int main()
{
	std::vector<int> vec = { 3,5,1,4,2 };
	std::sort(vec.begin(), vec.end(),std::greater<int>());
	for (int value : vec)
	{
		std::cout << value << std::endl;
	}
	std::cin.get();
	return 0;
}
```
如果使用lambda函数
```
#include <iostream>
#include <vector>
#include <algorithm>

int main()
{
	std::vector<int> vec = { 3,5,1,4,2 };
	std::sort(vec.begin(), vec.end(),[](int a,int b)
    {
	    return a < b;
    });
	for (int value : vec)
	{
		std::cout << value << std::endl;
	}
	std::cin.get();
	return 0;
}
```
比较函数应返回一个bool值，当需要第一个参数即a排在前面时则函数应该返回true，排在后面返回false