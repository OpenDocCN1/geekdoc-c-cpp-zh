```
class Shape {
public:
    Shape(const Shape&)=delete;      // no copying
    Shape& operator=(const Shape&)=delete;
    // ...
};
```

```
void copy(Shape& s1, const Shape& s2)
{
    s1 = s2; // error: Shape copy is deleted
}
```