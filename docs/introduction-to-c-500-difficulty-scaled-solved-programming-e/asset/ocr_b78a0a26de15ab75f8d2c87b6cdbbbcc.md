If the new value of the radius is negative, the function should create an int exception with code 10. If the type of c is Ellipse, the function should reduce the radius and axis of c by n. If the new value of either the radius or axis is negative, the function should create an int exception with code 10 and 20.

```
tmp.show(); /* If no exception is thrown, the program should display the values of the tmp members. In this example, in the first call of f(), the program should display 2 (5-3), in the second call it should display 9 (10-1) and 5 (6-1), while in the third call it must throw an exception code 20 since the new value of the axis is negative. */
}
```

Answer:

```
#include <iostream>
```

```
class Circle {
private:
    float rad;
public:
    Circle(float r) { rad = r; }
    virtual ~Circle() { }
    float get() const { return rad; }
    void set(float r) { rad = r; }
    virtual Circle& operator-(int n);
    virtual void show() const;
};
```

```
class Ellipse : public Circle {
private:
    float axis;
public:
    Ellipse(float r, float a) : Circle(r), axis(a) {}
    virtual Ellipse& operator-(int n) override;
    virtual void show() const override;
};
```

```
void f(Circle& c, int n);
```

```
Circle::operator-(int n) {
    rad = n;
    if(rad < 0)
        throw *this;
}
```

```
void Circle::show() const {
    std::cout << "R:" << rad << '\n';
}
```