```
```cpp
class point
{
public:
	point(int x, int y) : x(x), y(y) {}

	bool operator==(const point& that) const
	{ return x == that.x && y == that.y; }
private:
	int x, y;
};
```
```