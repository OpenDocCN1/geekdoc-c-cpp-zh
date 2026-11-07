```
```cpp
double getWidth() const;
    //Function to return the width of the rectangle.
    //Postcondition: The value of width is returned.

double area() const;
    //Function to return the area of the rectangle.
    //Postcondition: The area of the rectangle is
    //              calculated and returned.

double perimeter() const;
    //Function to return the perimeter of the rectangle.
    //Postcondition: The perimeter of the rectangle is
    //              calculated and returned.

void print() const;
    //Function to output the length and width of
    //the rectangle.

rectangleType();
    //Default constructor
    //Postcondition: length = 0; width = 0;

rectangleType(double l, double w);
    //Constructor with parameters
    //Postcondition: length = l; width = w;

private:
    double length;
    double width;
};
```
```

The definitions of the member functions of the `class rectangleType` are as follows:

```
```cpp
void rectangleType::setDimension(double l, double w)
{
    if (l >= 0)
        length = l;
    else
        length = 0;

    if (w >= 0)
        width = w;
    else
        width = 0;
}

double rectangleType::getLength() const
{
    return length;
}
```
```