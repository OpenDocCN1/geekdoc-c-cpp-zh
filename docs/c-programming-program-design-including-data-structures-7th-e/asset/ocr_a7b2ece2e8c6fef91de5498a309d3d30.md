```
```cpp
double rectangleType::getWidth() const
{
    return width;
}

double rectangleType::area() const
{
    return length * width;
}

double rectangleType::perimeter() const
{
    return 2 * (length + width);
}

void rectangleType::print() const
{
    cout << "Length = " << length
         << " Width = " << width;
}

rectangleType::rectangleType(double l, double w)
{
    setDimension(l, w);
}

rectangleType::rectangleType()
{
    length = 0;
    width = 0;
}
```
```

The **class** rectangleType has two private member variables: length and width, both of type **double**. We will add operator functions to the **class** rectangleType as we overload the operators.

Also, suppose that you have the following statements:

```
```cpp
rectangleType myRectangle;
rectangleType yourRectangle;
rectangleType tempRect;
```
```

That is, myRectangle, yourRectangle, and tempRect are objects of type rectangleType.

C++ consists of both binary and unary operators. It also has a ternary operator, ?, which *cannot* be overloaded. The next few sections discuss how to overload various binary and unary operators.