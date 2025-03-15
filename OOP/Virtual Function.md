### 虚函数(Virtual Function)
虚函数引入了动态联编(Dynamic Dispatch，指编译程序在编译阶段并不能确切地知道将要调用的函数，只有在程序执行时才能确定将要调用的函数)，
它通常通过虚函数表来实现编译，虚函数表包含基类中所有虚函数的映射，在运行时，将它们映射到正确的重写(override)函数。  
需要额外的内存来存储V表，基类中要有一个成员指针指向V表，每次调用虚函数时都需要遍历该表以确定要映射到哪个函数。
```
class Entity
{
public:
	virtual string GetName() { return "Entity"; }
};
class Player : public Entity
{
public:
	string GetName() override { return "Player"; }
};
void PrintName(Entity* entity)
{
	cout << entity->GetName() << endl;
}
int main()
{
	Entity* e = new Entity();
	Player* p = new Player();

	PrintName(e);
	PrintName(p);//如果不override虚函数，这里会打印出两个Entity

	cin.get();
	return 0;
}
```

### 纯虚函数(Pure Virtual Function)
在基类中定义一个没有实现的函数，然后强制子类去实现该函数。  
创建一个类（抽象类），只由未实现的方法组成，然后强制子类去实际实现它们，这通常被称为接口(Interface)，C++没有interface关键字。  
如果子类没有实现纯虚函数，则该子类不能被实例化
```
class Printable
{
public:
	virtual string GetClassName() = 0;
};
class A : public Printable
{
public:
	string GetClassName() override { return "A"; }
};

void Print(Printable* obj)
{
	cout << obj->GetClassName() << endl;
}
int main()
{
  Print(new A());
  return 0;
}
```
