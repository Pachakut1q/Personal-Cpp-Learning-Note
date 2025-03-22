### 模板(Template)
```
template<typename T> // or "template<class T>"
void Print(T value)
{
	std::cout << value << std::endl;
}
int main()
{
	Print(1); // or "Print<int>(1);"
	Print("test");
	Print(5.5f);

	std::cin.get();
	return 0;
}
```
函数Print()并不是一段实际的代码，只有在它被调用，根据传递的参数，创建出对应的函数并作为源代码被编译。
使用模板类：
```
template<typename T, int N>
class Array
{
private:
	T m_Array[N];
public:
	int GetSize() const { return N; }
};
int main()
{
	Array<std::string, 5> array;
	int size = array.GetSize();
	std::cout << size << std::endl;

	std::cin.get();
	return 0;
}
```