## 单例模式

```
class Random
{
public:
	Random(const Random&) = delete;//删除拷贝构造函数

	static Random& Get()
	{
		static Random instance;
		return instance;
	}//确保只能有一个实例

	static float Float() { return Get().m_RandomGenerator; }//假设这是一个随机数生成器
private:
	Random() {}//隐藏构造函数
	float m_RandomGenerator = 0.5f;
};
int main()
{
	float f = Random::Float();

	std::cin.get();
	return 0;
}
```
Random类也能写成：
```
class Random
{
public:
	Random(const Random&) = delete;//删除拷贝构造函数

	static Random& Get()
	{
		static Random instance;
		return instance;
	}//确保只能有一个实例

	static float Float() { return Get().IFloat(); }//多进行了一层包装
private:
	float IFloat() { return m_RandomGenerator; }
	Random() {}//隐藏构造函数
	float m_RandomGenerator = 0.5f;
};
```