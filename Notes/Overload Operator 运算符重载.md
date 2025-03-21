### 运算符重载
```
class Vector2
{
public:
	float x, y;

	Vector2(float x,float y) : x(x), y(y) { }

	Vector2 Add(const Vector2& other) const
	{
		return Vector2(x + other.x, y + other.y);
	}
	Vector2 operator+(const Vector2& other) const //overload
	{
		return Add(other);
	}

	Vector2 Multiply(const Vector2& other) const
	{
		return Vector2(x * other.x, y * other.y);
	}
	Vector2 operator*(const Vector2& other) const //overload
	{
		return Multiply(other);
	}
};

std::ostream& operator<<(std::ostream& stream, const Vector2& other) //对ostream的<<运算符重载
{
	stream << other.x << ", " << other.y;
	return stream;
}

int main()
{
	Vector2 position(4.0f, 4.0f);
	Vector2 speed(0.5f, 1.5f);
	Vector2 powerup(1.1f, 1.1f);

	Vector2 result1 = position.Add(speed.Multiply(powerup));
	Vector2 result2 = position + speed * powerup;

    std::cout << result2 << std::endl;

	cin.get();
	return 0;
}
```