### 宏定义
在项目属性 -> C/C++ -> 预处理器 -> 预处理器定义一栏中有系统自带的宏定义比如debug配置下的_DEBUG以及release配置下的NDEBUG
```
#ifdef _DEBUG
#define LOG(x) std::cout << x << std::endl
#else
#define LOG(x)
#endif

int main()
{
	LOG("debug");
	return 0;
}
```
在debug模式下，_DEBUG被定义，#define LOG(x) std::cout << x << std::endl这条宏定义会生效。在release模式下#define LOG(x)会生效即空语句。  
也可以在项目属性中自定义宏的值（系统自带的宏默认为1且应该不能改变数值）
```
#if PR_DEBUG == 2
#define LOG(x) std::cout << x << std::endl
#elif defined(NDEBUG)
#define LOG(x)
#endif
```