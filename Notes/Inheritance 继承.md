### 继承(Inheritance)
```
class Entity
{
public:
  floay X, Y;

  void Move(float xa, float ya)
  {
    X += xa;
    Y += ya;
  }
};

class Player : public Entity
{
public:
  const char* Name;

  void PrintName()
  {
    std::cout << Name << std::endl;
  }
};

int main()
{
  Player player;
  player.Move(5,5);
  player.X = 2;
  return 0;
}
```
