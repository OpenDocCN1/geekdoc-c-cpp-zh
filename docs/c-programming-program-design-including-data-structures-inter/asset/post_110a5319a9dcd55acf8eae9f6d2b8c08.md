
```cpp
cout << "Passing object myYard to the friend "
     << "function rectangleFriend." << endl;  //Line 10
rectangleFriend(myYard);                       //Line 11
return 0;                                      //Line 12
}                                              //Line 13
```

## Sample Run

```text
myYard area: 450.00
Passing object myYard to the friend function rectangleFriend.
recFriendObject area: 450.00
After increasing length and width by 5 units each,
    recFriendObject area: 690.00
```

For the most part, the output is self-explanatory. The statement in Line 9 outputs the area of myYard. The statement in Line 11 calls the function rectangleFriend (a friend function of the class rectangleType) and passes the object myYard as an actual parameter. Notice that the function rectangleFriend generates the last three lines of the output.

Later in this chapter, you will learn that for a class, stream insertion and extraction operators can be overloaded only as friend functions.

## Operator Functions as Member Functions and Nonmember Functions

The beginning of this chapter stated that certain rules must be followed when you include an operator function in the definition of a class. This section describes these rules.

Most operator functions can be either member functions or nonmember functions—that is, friend functions of a class. To make an operator function be a member or nonmember function of a class, keep the following in mind:

- 1. The function that overloads any of the operators `()`, `[]`, `->`, or `=` for a class must be declared as a member of the class.
- 2. Suppose that an operator op is overloaded for a class—say, opOverClass. (Here, op stands for an operator that can be overloaded, such as `+` or `>>`.)
  - a. If the far left operand of op is an object of a different type (that is, not of type opOverClass), the function that overloads the operator op for opOverClass must be a nonmember—that is, a friend of the class opOverClass.
  - b. If the operator function that overloads the operator op for the class opOverClass is a member of the class opOverClass, then when applying op on objects of type opOverClass, the far left operand of op must be of type opOverClass.

```cpp
private:
    double length;
    double width;
};
```

The definitions of the member functions of the class rectangleType are as follows:

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
         << "; Width = " << width;
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

The class rectangleType has two private member variables: length and width, both of type double. We will add operator functions to the class rectangleType as we overload the operators.

Also, suppose that you have the following statements:

```cpp
rectangleType myRectangle;
rectangleType yourRectangle;
rectangleType tempRect;
```

That is, myRectangle, yourRectangle, and tempRect are objects of type rectangleType.

C++ consists of binary and unary operators. It also has a ternary operator, which cannot be overloaded. The next few sections discuss how to overload various binary and unary operators.

## Overloading Binary Operators

Suppose that # represents a binary operator (arithmetic, such as +; or relational, such as ==) that is to be overloaded for the class rectangleType. This operator can be overloaded as either a member function of the class or as a friend function. We will describe both ways to overload this operator.

### OVERLOADING THE BINARY OPERATORS AS MEMBER FUNCTIONS

Suppose that # is overloaded as a member function of the class rectangleType. The name of the function to overload # for the class rectangleType is:

```cpp
operator#
```

Because myRectangle and yourRectangle are objects of type rectangleType, you can perform the operation:

```cpp
myRectangle # yourRectangle
```

The compiler translates this expression into the following expression:

```cpp
myRectangle.operator#(yourRectangle)
```

This expression clearly shows that the function operator# has only one parameter, which is yourRectangle.

Because operator# is a member of the class rectangleType and myRectangle is an object of type rectangleType, in the previous statement, operator# has direct access to the private members of the object myRectangle. Thus, the first parameter of operator# is the object that is invoking the function operator#, and the second parameter is passed as a parameter to this function.

### GENERAL SYNTAX TO OVERLOAD THE BINARY (ARITHMETIC OR RELATIONAL) OPERATORS AS MEMBER FUNCTIONS

This section describes the general form of the functions to overload the binary operators as member functions of a class.

**Function Prototype** (to be included in the definition of the class):

```cpp
returnType operator#(const className&) const;
```

in which # stands for the binary operator, arithmetic or relational, to be overloaded; returnType is the type of value returned by the function; and className is the name of the class for which the operator is being overloaded.

**Function Definition:**

```cpp
returnType className::operator#
                (const className& otherObject) const
{
    //algorithm to perform the operation

    return value;
}
```

> The return type of the functions that overload relational operators is bool.

### EXAMPLE 13-4.

Let us overload +, *, ==, and != for the class rectangleType. These operators are overloaded as member functions.

```cpp
class rectangleType
{
public:
    void setDimension(double l, double w);
    double getLength() const;
    double getWidth() const;
    double area() const;
    double perimeter() const;
    void print() const;

    rectangleType operator+(const rectangleType&) const;
    //Overload the operator +
    rectangleType operator*(const rectangleType&) const;
    //Overload the operator *

    bool operator==(const rectangleType&) const;
    //Overload the operator ==
    bool operator!=(const rectangleType&) const;
    //Overload the operator !=

    rectangleType();
    rectangleType(double l, double w);

private:
    double length;
    double width;
};
```

The definition of the function operator+ is as follows:

```cpp
rectangleType rectangleType::operator+
                   (const rectangleType& rectangle) const
{
    rectangleType tempRect;

    tempRect.length = length + rectangle.length;
    tempRect.width = width + rectangle.width;

    return tempRect;
}
```

Notice that operator+ adds the corresponding lengths and widths of the two rectangles. The definition of the function operator* is as follows:

```cpp
rectangleType rectangleType::operator*
                   (const rectangleType& rectangle) const
{
    rectangleType tempRect;

    tempRect.length = length * rectangle.length;
    tempRect.width = width * rectangle.width;

    return tempRect;
}
```

Notice that operator* multiplies the corresponding lengths and widths of the two rectangles. Two rectangles are equal if their lengths and widths are equal. Therefore, the definition of the function to overload the operator == is:

```cpp
bool rectangleType::operator==
                   (const rectangleType& rectangle) const
{
    return (length == rectangle.length &&
            width == rectangle.width);
}
```

Two rectangles are not equal if either their lengths are not equal or their widths are not equal. Therefore, the definition of the function to overload the operator != is:
