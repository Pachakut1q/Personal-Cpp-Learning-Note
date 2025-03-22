### 关键字 this
this是一个指向当前对象实例的 指针 。
```
void PrintEntity(const Entity& e);

class Entity
{
public:
	int x, y;

	Entity(int x, int y)
	{
		this->x = x; // or (*this).x = x;
		this->y = y; // or (*this).y = y;

		PrintEntity(*this);
	}

};
void PrintEntity(const Entity& e)
{
	//do something
}
```