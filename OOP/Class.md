### 类(Class)与结构(Struct)的比较  
技术上没有区别。
Class默认为private；Struct默认为public  
Struct中同样可以创建函数。  
Struct无法使用继承，更具体地讲，struct更适合于仅存储一些数据，当需要一个包含很多功能的“系统”时class更好。  
  
### 构造函数(constructor)
构造函数是一种特殊类型的方法，它在每次实例化对象时运行。  
C++为类提供了默认构造函数，一般需要进行重载(overload)
只是用类的静态方法时不会被调用。  
```
class Entity
{
public:
	float X, Y;
	Entity() 
	{
		X = 1;
		Y = 2;//可以为空函数体，这时候实例化该类并调用Print时显示的就是X,Y的内存空间中原本的值
	}
	Entity(float x, float y) //overload
	{
		X = x;
		Y = y;
	}
	void Print()
	{
		cout << X << "," << Y << endl;
	}
};
```

### 析构函数(distructor)
在销毁对象时被调用。  
如果在堆(heap)上手动分配了任何类型的内存，那么则需要手动清理，此时就可以利用析构函数。
```
~Entity()
{
	//Do something
}
```
