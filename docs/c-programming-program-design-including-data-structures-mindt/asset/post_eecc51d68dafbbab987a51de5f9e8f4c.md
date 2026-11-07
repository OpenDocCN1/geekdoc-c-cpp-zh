
Now consider the following statement:

```cpp
cout << myRectangle << yourRectangle;
```

This statement is equivalent to the statement

```cpp
operator<<(operator<<(cout, myRectangle), yourRectangle); //line A
```

because the associativity of the operator << is from left to right.

To execute the previous statement, you must first execute the expression

```cpp
cout << myRectangle
```

that is, the expression

```cpp
operator<<(cout, myRectangle)
```

After executing this expression, which outputs the value of myRectangle, whatever is returned by the function operator<< will become the left-side parameter of the operator << (that is, the first parameter of the function operator<<) in order to output the value of object yourRectangle (see the statement in Line A). The left-side parameter of the operator << must be an object of the ostream type, so the expression

```cpp
cout << myRectangle
```

must return the object cout (not its value) to the left side of the second operator << in order to output the value of yourRectangle.

Therefore, the return type of the function operator<< must be a reference to an object of the ostream type.

## Overloading the Stream Extraction Operator (>>)

The general syntax to overload the stream extraction operator, >>, for a class is described next. **Function Prototype** (to be included in the definition of the class):

```cpp
friend istream& operator>>(istream&, className&);
```

### Function Definition:

```cpp
istream& operator>>(istream& isObject, className& cObject)
{
    //local declaration, if any
    //Read the data into cObject.
    //isObject >> ...

    //Return the stream object.
    return isObject;
}
```

In this function definition:

- Both parameters are reference parameters.
- The first parameter—that is, `isObject`—is a reference to an `istream` object.
- The second parameter is usually a reference to a particular class. The data read will be stored in the object.
- The function return type is a reference to an `istream` object.

For the same reasons as explained previously (when we overloaded the insertion operator `<<`), the return type of the function `operator>>` must be a reference to an `istream` object. We can then successfully execute statements of the following type:

```cpp
cin >> myRectangle >> yourRectangle;
```

Example 13-7 shows how the stream insertion and extraction operators are overloaded for the `class rectangleType`.

### Example 13-7

The definition of the `class rectangleType` and the definitions of the operator functions are as follows:

```cpp
#include <iostream>

using namespace std;

class rectangleType
{
    //Overload the stream insertion and extraction operators
    friend ostream& operator<< (ostream&, const rectangleType &);
    friend istream& operator>> (istream&, rectangleType &);

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
};
```

```cpp
cin >> yourRectangle;
cout << endl;

cout << "Line 12: yourRectangle: "
     << yourRectangle << endl;

cout << "Line 13: myRectangle + yourRectangle: "
     << myRectangle + yourRectangle << endl;
cout << "Line 14: myRectangle * yourRectangle: "
     << myRectangle * yourRectangle << endl;

return 0;
}
```

**Sample Run:** In this sample run, the user input is shaded.

```text
Line 8: myRectangle: Length = 23; Width = 45
Line 9: Enter the length and width of a rectangle: 28 17

Line 12: yourRectangle: Length = 28; Width = 17
Line 13: myRectangle + yourRectangle: Length = 51; Width = 62
Line 14: myRectangle * yourRectangle: Length = 644; Width = 765
```

The statements in Lines 6 and 7 declare and initialize myRectangle and yourRectangle to be objects of type rectangleType. The statement in Line 8 outputs the value of myRectangle using cout and the insertion operator. The statement in Line 10 inputs the data into yourRectangle using cin and the extraction operator. The statement in Line 12 outputs the value of yourRectangle using cout and the insertion operator. The cout statement in Line 13 adds the lengths and widths of myRectangle and yourRectangle and outputs the result. Similarly, the cout statement in Line 14 multiplies the lengths and widths of myRectangle and yourRectangle and outputs the result. The output shows that both the stream insertion and stream extraction operators were overloaded successfully.

### Overloading the Assignment Operator (=)

One of the built-in operations on classes is the assignment operation. The assignment operator causes a member-wise copy of the member variables of the class. For example, the statement

```cpp
myRectangle = yourRectangle;
```

is equivalent to the statements

```cpp
myRectangle.length = yourRectangle.length;
myRectangle.width = yourRectangle.width;
```

From Chapter 12, recall that the built-in assignment operator works well for classes that do not have pointer member variables, but not for classes with pointer member variables. Therefore, to avoid the shallow copy of data for classes with pointer member variables, we must explicitly overload the assignment operator.

Recall that to overload the assignment operator `=` for a class, the operator function `operator=` must be a member of that class.

### General Syntax to Overload the Assignment Operator `=` for a Class

The general syntax to overload the assignment operator `=` for a class is described next.

**Function Prototype** (to be included in the definition of the class):

```cpp
const className& operator=(const className&);
```

### Function Definition:

```cpp
const className& className::operator=
                    (const className& rightObject)
{
    //local declaration, if any

    if (this != &rightObject)//avoid self-assignment
    {
        //algorithm to copy rightObject into this object
    }

        //Return the object assigned.
    return *this;
}
```

In the definition of the function `operator=`:

- There is only one formal parameter.
- The formal parameter is usually a `const` reference to a particular class.
- The function return type is a `const` reference to a particular class.

We now explain why the return type of the function `operator=` should be a reference of the class type.

Suppose that the assignment operator `=` is overloaded for the class `rectangleType`.

The statement

```cpp
myRectangle = yourRectangle;
```

is equivalent to the statement

```cpp
myRectangle.operator=(yourRectangle);
```

That is, the object `yourRectangle` becomes the actual parameter to the function `operator=`

Now consider the statement:

```cpp
myRectangle = yourRectangle = tempRect;
```

## Mixed Effects Models for Complex Data

Richard A. Berk

> "An insightful and thorough treatment of mixed effects models for a wide range of applications."

This book provides a comprehensive introduction to mixed effects models, emphasizing practical data analysis and interpretation. It covers linear, generalized linear, and nonlinear mixed effects models, with detailed discussion of estimation, inference, and model checking.

- Balanced treatment of theory and applications
- Examples from ecology, medicine, and social sciences
- Emphasis on model diagnostics and interpretation

![](img/b217c421655b51e7494cf3b89bb5432d_986_0.png)

| Chapter | Topic | Pages |
|---------|-------|-------|
| 1       | Introduction | 1–15 |
| 2       | Linear Mixed Models | 16–42 |
| 3       | Generalized Linear Mixed Models | 43–70 |

```r
library(lme4)
model <- lmer(Reaction ~ Days + (1 | Subject), data = sleepstudy)
summary(model)
```
