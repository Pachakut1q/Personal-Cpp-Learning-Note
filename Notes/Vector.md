### Vector
vector 是 C++ 标准模板库（STL）的一部分，它是一种序列容器，它允许你在运行时动态地插入和删除元素。vector 是基于数组的数据结构，但它可以自动管理内存。  
当使用Vector时超过了分配的大小，它会在内存中创建一个比第一个大的新数组，把所有东西复制进去，再删除旧数组。
```
struct Vertex
{
	float x, y, z;
};
std::ostream& operator<<(std::ostream& stream, const Vertex& vertex)
{
	stream << vertex.x << ", " << vertex.y << ", " << vertex.z;
	return stream;
}
int main()
{
	std::vector<Vertex> vec;
	vec.push_back({ 1,2,3 });
	vec.push_back({ 4,5,6 });

	for (int i = 0; i < vec.size(); i++)
		std::cout << vec[i] << std::endl;

	vec.erase(vec.begin() + 1);
	for (Vertex v : vec)
		std::cout << v << std::endl;

	std::cin.get();
	return 0;
}
```
控制台打印：
```
1, 2, 3
4, 5, 6
1, 2, 3
```
### 一点优化策略
```
struct Vertex
{
	float x, y, z;
	Vertex(float x, float y, float z) :x(x), y(y), z(z) {}
	Vertex(const Vertex& vertex)
		:x(vertex.x), y(vertex.y), z(vertex.z)
	{
		std::cout << "Copied" << std::endl;
	}
};
int main()
{
	std::vector<Vertex> vec;
	vec.push_back(Vertex(1, 2, 3));
    vec.push_back(Vertex(4, 5, 6));
    //vec.push_back(Vertex(7, 8, 9));

	std::cin.get();
	return 0;
}
```
控制台会打印3次Copied（如果去掉注释一行，则会打印6次）：  
vector 的内存管理是这样的，在插入元素时，如果当前容量不足，会重新分配更大的内存空间，并将原有元素逐个拷贝到新内存，然后销毁旧内存。这会触发额外的拷贝构造函数调用。而当调用 vec.push_back(Vertex(1, 2, 3))时，会显式构造一个 Vertex 的临时对象。这个临时对象会被拷贝到 vector 的内存中，也会触发一次拷贝构造函数。  
vec.push_back(Vertex(1, 2, 3));显式构造Copy一次  
vec.push_back(Vertex(4, 5, 6));发现内存不够，进行扩容分配新内存，拷贝旧元素Copy一次，构造临时对象{4, 5, 6}拷贝到新内存Copy一次，共三次。  
优化：
```
std::vector<Vertex> vec;
vec.reserve(3);
vec.emplace_back(1, 2, 3);
vec.emplace_back(4, 5, 6);
vec.emplace_back(7, 8, 9);
```
reserve(): reserve的作用是更改vector的容量（capacity），使vector至少可以容纳n个元素。
如果n大于vector当前的容量，reserve会对vector进行扩容。其他情况下都不会重新分配vector的存储空间,也就避免了扩容后再次调用拷贝构造函数。当然这是建立在已知需要多少空间的情况下。  
emplace_back():将参数列表传递给vector，使用该列表直接构造一个Vertex对象，避免了push_back需要先构造一个临时对象的拷贝。  
优化后控制台Copied输出次数为0。
