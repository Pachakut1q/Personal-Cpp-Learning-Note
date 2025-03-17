### 类(Class)与结构(Struct)的比较  
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
### 可见性(Visibility)
1.类的一个特征就是封装，public和private作用就是实现这一目的。  
用户代码（类外）可以访问public成员而不能访问private成员；private成员只能由类成员（类内）和友元（friend）访问。  
2.类的另一个特征就是继承，protected的作用就是实现这一目的。  
protected成员可以被派生类对象访问，不能被用户代码（类外）访问。
### 构造函数初始化列表(initializer list)
```
class Example
{
public:
	Example()
	{
		cout << "Created Entity!" << endl;
	}

	Example(int x)
	{
		cout << "Created Entity with " << x << "!" << endl;
	}
};

class Entity
{
private:
	string m_Name;
	Example m_Example;
public:
	Entity()
	{
		m_Name = "Unknown";//相当于m_Name = string("Unknown")
		m_Example = Example(8);
	}
};

int main()
{
	Entity e;

	cin.get();
}
```
如果运行上面的例子，则会在控制台中看到  
Created Entity!  
Created Entity with 8!  
因为在这个例子中m_Example是Entity的成员，在创建Entity实例时会先调用Example的默认构造函数，然后在Entity的构造函数中又调用了Example带参数的构造函数，也就是先后创建了两个对象，只不过后一个对象覆盖了前者，这会导致性能浪费。对m_Name变量也同理。  
使用列表初始化：
```
class Entity
{
private:
	string m_Name;
	Example m_Example;
public:
	Entity() : m_Name("name"), m_Example(6)//一定要按照声明顺序
	{
	}
};
```
则只会出现Created Entity with 6!
### 创建对象
两种方式  
```
//堆对象（需手动释放）
Entity* e = new Entity();
e->GetName();  //通过指针访问
delete e;      //必须手动释放否则发生内存泄漏
/*
Entity* e2 = e;
delete e2;	   //e和e2指向的是同一处堆内存空间，只需要delete其中一个即可
*/
//栈对象（自动释放）
Entity e1 = Entity();//just "Entity e1" in C++17
e1.GetName();  //直接访问
// e1 在离开作用域时自动调用析构函数
```
如何选择？对象太大或显式控制对象的生存期就在heap上创建，否则创建在stack