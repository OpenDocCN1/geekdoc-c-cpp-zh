```
struct Circle
{
  float diam;
  float area;
};
```

```
struct Square
{
  float side;
  float area;
  struct Circle innercircle;
  struct Circle outercircle;
};
```

Given the length of the side of a square, an instance of the structure Square area can be defined. The length of the side of the square can be used to determine the area of the square and the two instances of the structure Circle, one of which describes the circle inscribed in the square and the other of which describes a circle circumscribed around the square. The code would be as follows:

```
int main()
{
  const float PI = 3.141593;
  struct Square box;
  float x, s;

  scanf("%f", &x);
  box.side = x;
  box.area = x * x;
  box.innercircle.area = PI * x * x / 4.0;
  s = sqrt(2.0 * x * x);
  box.outercircle.diam = s;
  box.outercircle.area = PI * s * s / 4.0;

  return 0;
}
```

If instead of declaring two members of the structure Square as Circle, they were declared as pointers to circles, the declaration of a Square and definition of an instance of square would require the definition of two instances of a Circle as follows: