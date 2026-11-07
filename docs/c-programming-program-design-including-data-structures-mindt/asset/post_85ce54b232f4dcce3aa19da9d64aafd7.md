
## PROGRAMMING EXAMPLE: Complex Numbers

A number of the form $a + ib$, in which $i^2 = -1$ and $a$ and $b$ are real numbers, is called a complex number. We call $a$ the real part and $b$ the imaginary part of $a + ib$. Complex numbers can also be represented as ordered pairs $(a, b)$. The addition and multiplication of complex numbers are defined by the following rules:

$(a + ib) + (c + id) = (a + c) + i(b + d)$

$(a + ib)(c + id) = (ac - bd) + i(ad + bc)$

Using the ordered pair notation, these rules are written as:

$(a, b) + (c, d) = ((a + c), (b + d))$

$(a, b) * (c, d) = ((ac - bd), (ad + bc))$

C++ has no built-in data type that allows us to manipulate complex numbers. In this example, we will construct a data type, `complexType`, that can be used to process complex numbers. We will overload the stream insertion and stream extraction operators for easy input and output. We will also overload the operators + and * to perform addition and multiplication of complex numbers. If $x$ and $y$ are complex numbers, we can evaluate expressions such as $x + y$ and $x * y$.

The definition of the class `complexType` is:

```cpp
#include <iostream>
using namespace std;

class complexType
{
    //Overload the stream insertion and extraction operators
    friend ostream& operator<<(ostream&, const complexType&);
    friend istream& operator>>(istream&, complexType&);

public:
    void setComplex(const double& real, const double& imag);
        //Function to set the complex numbers according to
        //the parameters.
        //Postcondition: realPart = real; imaginaryPart = imag;

    void getComplex(double& real, double& imag) const;
        //Function to retrieve the complex number.
        //Postcondition: real = realPart; imag = imaginaryPart;

    complexType(double real = 0, double imag = 0);
        //Constructor
        //Initializes the complex number according to
        //the parameters.
        //Postcondition: realPart = real; imaginaryPart = imag;

    complexType operator+
                (const complexType& otherComplex) const;
    //overload the operator +

    complexType operator*
                (const complexType& otherComplex) const;
    //overload the operator *

    bool operator== (const complexType& otherComplex) const;
    //overload the operator ==

private:
    double realPart;       //variable to store the real part
    double imaginaryPart;  //variable to store the
                           //imaginary part
};
```

Figure 13-2 shows a UML class diagram of the class `complexType`.

![](img/b217c421655b51e7494cf3b89bb5432d_1009_0.png)

FIGURE 13-2  UML class diagram of the class `complexType`

Next, we write the definitions of the functions to implement various operations of the class `complexType`.

The definitions of most of these functions are straightforward. We will discuss only the definitions of the functions to overload the stream insertion operator, `<<`, and the stream extraction operator, `>>`.

To output a complex number in the form:

`(a, b)`

```cpp
isObject >> complex.imaginaryPart;        //Step d
isObject >> ch;                            //Step e

}
return isObject;  //return the istream object
```

The definitions of the other functions are as follows:

```cpp
bool complexType::operator==
                    (const complexType& otherComplex) const
{
    return (realPart == otherComplex.realPart &&
            imaginaryPart == otherComplex.imaginaryPart);
}

//constructor
complexType::complexType(double real, double imag)
{
    realPart = real;
    imaginaryPart = imag;
}

//Function to set the complex number after the object
//has been declared
void complexType::setComplex(const double& real,
                             const double& imag)
{
    realPart = real;
    imaginaryPart = imag;
}

void complexType::getComplex(double& real, double& imag) const
{
    real = realPart;
    imag = imaginaryPart;
}

//overload the operator +
complexType complexType::operator+
                    (const complexType& otherComplex) const
{
    complexType temp;

    temp.realPart = realPart + otherComplex.realPart;
    temp.imaginaryPart = imaginaryPart
                       + otherComplex.imaginaryPart;

    return temp;
}

//overload the operator *
complexType complexType::operator*
                         (const complexType& otherComplex) const
{
    complexType temp;
    temp.realPart = (realPart * otherComplex.realPart)
                  - (imaginaryPart * otherComplex.imaginaryPart);
    temp.imaginaryPart = (realPart * otherComplex.imaginaryPart)
                       + (imaginaryPart * otherComplex.realPart);
    return temp;
}
```

The following program illustrates the use of the class complexType:

```cpp
//**************************************************************
// Author: D.S. Malik
//
// This program shows how to use the class complexType.
//**************************************************************

#include <iostream>                                  //Line 1
#include "complexType.h"                             //Line 2

using namespace std;                                  //Line 3

int main()                                           //Line 4
{                                                    //Line 5
        complexType num1(21, 18);                    //Line 6
        complexType num2;                             //Line 7
        complexType num3;                             //Line 8

        cout << "Line 9: Num1 = " << num1 << endl;  //Line 9
        cout << "Line 10: Num2 = " << num2 << endl; //Line 10

        cout << "Line 11: Enter a complex number "  //Line 11
             << "in the form (a, b): ";             
        cin >> num2;                                 //Line 12
        cout << endl;                                 //Line 13

        cout << "Line 14: New value of num2 = "     
             << num2 << endl;                         //Line 14

        num3 = num1 + num2;                           //Line 15

        cout << "Line 16: Num3 = " << num3 << endl;  //Line 16
        cout << "Line 17: " << num1 << " + " << num2
             << " = " << num1 + num2 << endl;        //Line 17

        cout << "Line 18: " << num1 << " * " << num2
             << " = " << num1 * num2 << endl;        //Line 18

        return 0;                                     //Line 19
}                                                    //Line 20
```

Sample Run: In this sample run, the user input is shaded.

```text
Line 9: Num1 = (21, 18)
Line 10: Num2 = (0, 0)
Line 11: Enter a complex number in the form (a, b): (5, 9)

Line 14: New value of num2 = (5, 9)
Line 16: Num3 = (26, 27)
Line 17: (21, 18) + (5, 9) = (26, 27)
Line 18: (21, 18) * (5, 9) = (-57, 279)
```

You can extend this data type to perform subtraction and division on complex numbers.

Next, we will define a class, called `newString`, and overload the assignment and relational operators. That is, when we declare a variable of type `newString`, we will be able to use the assignment operator to copy one string into another and relational operators to compare the two strings.

Before discussing the class `newString`, however, we will examine the overloading of the operator `[]`. Recall that we have used the operator `[]` to access the components of an array. To access individual characters in a string of type `newString`, we have to overload the operator `[]` for the class `newString`.

### Overloading the Array Index (Subscript) Operator ([])

Recall that the function to overload the operator `[]` for a class must be a member of the class. Furthermore, because an array can be declared as constant or nonconstant, we need to overload the operator `[]` to handle both cases.

The syntax to declare the operator function `operator[]` as a member of a class for nonconstant arrays is:

```cpp
Type& operator[](int index);
```

The syntax to declare the operator function `operator[]` as a member of a class for constant arrays is:

```cpp
const Type& operator[](int index) const;
```

in which `Type` is the data type of the array elements.

Suppose that `classTest` is a class that has an array member variable. The definition of `classTest` to overload the operator `[]` is:
