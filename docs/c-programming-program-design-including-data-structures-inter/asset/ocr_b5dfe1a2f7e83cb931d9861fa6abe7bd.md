length and width to 0.00, and 0.00, respectively. The statement in Line 10 outputs the area of oldYard. The statement in Line 11 doubles the dimensions of oldYard and then the object oldYard, with new length and width, is returned by the pointer this. The statement in Line 12 outputs the area of newYard.

The following example shows another way of how the pointer `this` works.

# EXAMPLE 17-2

Consider the following class:

```
class rectangleType
{
public:
    void setDimension (double l, double w);
    double getLength() const;
    double getWidth() const;
    double area() const;
    double perimeter() const;
    void print() const;

    rectangleType setLength(double l);
    //Function to set the length.
    //Postcondition: length = l
    //              After setting the length, a reference to the object,
    //              that is, the address of the object, is returned.
    rectangleType setWidth(double w);
    //Function to set the width.
    //Postcondition: width = w
    //              After setting the width a reference to the object,
    //              that is, the address of the object, is returned.

    rectangleType(double l = 0.0, double w = 0.0);

private:
    double length;
    double width;
};
```

Note that the definition of the class rectangleType is the same as given in Chapter 11, except that here, in the definition of the class rectangleType, we have added the functions setLength and setWidth to individually set a rectangle’s length and width, and then return the entire object. We have also replaced the constructors with the constructor with default parameters.

The definitions of the functions print, setDimension, getLength, getWidth, area, and perimeter are the same as before. The definition of the constructor with default parameters is the same as the definition of the constructor with parameters. The definitions of the functions setLength and setWidth are as follows: