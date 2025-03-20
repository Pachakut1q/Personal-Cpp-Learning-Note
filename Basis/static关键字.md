### 关键字static
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
