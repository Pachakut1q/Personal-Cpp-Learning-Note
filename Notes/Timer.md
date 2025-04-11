### Timer
利用C++11的chrono库，构造一个简单的计时器
```
struct Timer
{
	std::chrono::time_point<std::chrono::steady_clock> start, end;
	std::chrono::duration<float> duration;

	Timer() 
	{
		start = std::chrono::high_resolution_clock::now();
	}
	~Timer()
	{
		end = std::chrono::high_resolution_clock::now();
		duration = end - start;
		float ms = duration.count() * 1000.0f;
		std::cout << "Timer took " << ms << "ms" << std::endl;
	}
};

void function()
{
	Timer timer;
	for (int i = 0; i < 100; i++)
	{
		std::cout << "function\n"; //用“\n”比“std::endl”快很多
	}
}
int main()
{
	function();
	std::cin.get();
	return 0;
}
```