# **Program 7.1** Creating and handling two circle objects (Continued)

```
```cpp
// Definition of getArea member function
double Circle :: getArea () const
{
    const double PI = 3.14;
    return (PI * radius * radius);
}
// Definition of getPerimeter member function
double Circle :: getPerimeter () const
{
    const double PI = 3.14;
    return (2 * PI * radius);
}
// Definition of setRadius member function
void Circle :: setRadius (double value)
{
    radius = value;
}
/********************************************************
 * Application section: Objects are instantiated in this section.    *
 * Objects use member functions to get or set their attributes.      *
 ********************************************************/
int main ()
{
    // Creating first circle and applying member functions
    cout << "Circle 1: " << endl;
    Circle circle1;
    circle1.setRadius (10.0);
    cout << "Radius: " << circle1.getRadius() << endl;
    cout << "Area: " << circle1.getArea() << endl;
    cout << "Perimeter: " << circle1.getPerimeter() << endl << endl;
    // Creating second circle and applying member functions
    cout << "Circle 2: " << endl;
    Circle circle2;
    circle2.setRadius (20.0);
    cout << "Radius: " << circle2.getRadius() << endl;
    cout << "Area: " << circle2.getArea() << endl;
    cout << "Perimeter: " << circle2.getPerimeter();
    return 0;
}
```
```

```
```text
Run:
Circle 1:
Radius: 10
Area: 314
Perimeter: 62.8
```
```