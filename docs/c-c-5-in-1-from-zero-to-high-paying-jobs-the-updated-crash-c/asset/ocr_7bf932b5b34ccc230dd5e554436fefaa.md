```
~~~cpp
        double calculatePerimeter() const override {
            return 2 * 3.14159 * radius;
        }
};

class Triangle : public Shape {
private:
    double sideA, sideB, sideC;

public:
    Triangle(double a, double b, double c) : sideA(a), sideB(b), sideC(c) {}

    double calculateArea() const override {
        // Calculate area using Heron's formula
        double s = (sideA + sideB + sideC) / 2;
        return sqrt(s * (s - sideA) * (s - sideB) * (s - sideC));
    }

    double calculatePerimeter() const override {
        return sideA + sideB + sideC;
    }
};
~~~
```

```
~~~cpp
class Rectangle : public Shape {
private:
    double width;
    double height;

public:
    Rectangle(double w, double h) : width(w), height(h) {}

    double calculateArea() const override {
        return width * height;
    }

    double calculatePerimeter() const override {
        return 2 * (width + height);
    }
};

class Circle : public Shape {
private:
    double radius;

public:
    Circle(double r) : radius(r) {}
~~~
```