
almost create a new language of our own by the creative use of the function and operator overloading techniques. We can overload (give additional meaning to) all the C++ operators except the following:

+   - Class member access operators (., .*).
+   - Scope resolution operator (::).
+   - Size operator (sizeof).
+   - Conditional operator (?:).

The excluded operators are very few when compared to the large number of operators which qualify for the operator overloading definition.

Although the *semantics* of an operator can be extended, we cannot change its *syntax*, the grammatical rules that govern its use such as the number of operands, precedence and associativity. For example, the multiplication operator will enjoy higher precedence than the addition operator. Remember, when an operator is overloaded, its original meaning is not lost. For instance, the operator +, which has been overloaded to add two vectors, can still be used to add two integers.

## 7.2 Defining Operator Overloading

To define an additional task to an operator, we must specify what it means in relation to the class to which the operator is applied. This is done with the help of a special function, called *operator function*, which describes the task. The general form of an operator function is:

```
return type classname :: operator op(arglist)
{
    Function body        // task defined
}
```

where *return type* is the type of value returned by the specified operation and *op* is the operator being overloaded. The *op* is preceded by the keyword **operator**. **operator op** is the function name.

Operator functions must be either member functions (non-static) or friend functions. A basic difference between them is that a friend function will have only one argument for unary operators and two for binary operators, while a member function has no arguments for unary operators and only one for binary operators. This is because the object used to invoke the member function is passed implicitly and therefore is available for the member function. This is not the case with **friend** functions. Arguments may be passed either by value or by reference. Operator functions are declared in the class using prototypes as follows:

```
vector operator+(vector);                // vector addition
vector operator-();                       // unary minus
friend vector operator+(vector,vector);   // vector addition
friend vector operator-(vector);          // unary minus
vector operator-(vector &a);              // subtraction
int operator==(vector);                   // comparison
friend int operator==(vector,vector)      // comparison
```

**vector** is a data type of **class** and may represent both magnitude and direction (as in physics and engineering) or a series of points called elements (as in mathematics)

The process of overloading involves the following steps:

+   1. Create a class that defines the data type that is to be used in the overloading operaion.
+   2. Declare the operator function **operator** op() in the public part of the class. It may be either a member function or a **friend** function.
+   3. Define the operator function to implement the required operations.

Overloaded operator functions can be invoked by expressions such as

```
op x or x op
```

for unary operators and

```
x op y
```

for binary operators. op x (or x op) would be interpreted as

```
operator op (x)
```

for **friend** functions. Similarly, the expression x op y would be interpreted as either

```
x.operator op (y)
```

in case of member functions, or

```
operator op (x,y)
```

in case of **friend** functions. When both the forms are declared, standard argument matching is applied to resolve any ambiguity.

## 7.3 Overloading Unary Operators

Let us consider the unary minus operator. A minus operator when used as a unary, takes just one operand. We know that this operator changes the sign of an operand when applied to a basic data item. We will see here how to overload this operator so that it can be applied

to an object in much the same way as is applied to an int or float variable. The unary minus when applied to an object should change the sign of each of its data items.

Program 7.1 shows how the unary minus operator is overloaded.

```
```cpp
#include <iostream>

using namespace std;

class space
{
    int x;
    int y;
    int z;

public:
    void getdata(int a, int b, int c);
    void display(void);
    void operator-(); // overload unary minus
};

void space :: getdata(int a, int b, int c)
{
    x = a;
    y = b;
    z = c;
}

void space :: display(void)
{
    cout << x << " ";
    cout << y << " ";
    cout << z << "\n";
}

void space :: operator-()
{
    x = -x;
    y = -y;
    z = -z;
}

int main()
{
    space S;
    S.getdata(10, -20, 30);
}
```
```

```
cout << "S : ";
S.display();

-S;        // activates operator-() function

cout << "S : ";
S.display();

return 0;
}
```

PROGRAM 7.1

The Program 7.1 produces the following output:

S : 10 -20 30
S : -10 20 -30

> note
> The function operator -() takes no argument. Then, what does this operator function do?. It changes the sign of data members of the object S. Since this function is a member function of the same class, it can directly access the members of the object which activated it.

Remember, a statement like

```
S2 = -S1;
```

will not work because, the function operator-() does not return any value. It can work if the function is modified to return an object.

It is possible to overload a unary minus operator using a friend function as follows:

```
friend void operator-(space &s);          // declaration
void operator-(space &s)                 // definition
{
    s.x = -s.x;
    s.y = -s.y;
    s.z = -s.z;
}
```

> note
> Note that the argument is passed by reference. It will not work if we pass argument by value because only a copy of the object that activated the call is passed to operator-(). Therefore, the changes made inside the operator function will not reflect in the called object.

## 7.4 Overloading Binary Operators

We have just seen how to overload an unary operator. The same mechanism can be used to overload a binary operator. In Chapter 6, we illustrated, how to add two complex numbers using a friend function. A statement like

```
C = sum(A, B);        // functional notation.
```

was used. The functional notation can be replaced by a natural looking expression

```
C = A + B;            // arithmetic notation
```

by overloading the + operator using an operator+() function. The Program7.2 illustrates how this is accomplished.

# OVERLOADING + OPERATOR

```
#include <iostream>

using namespace std;

class complex
{
    float x;                    // real part
    float y;                    // imaginary part
public:
    complex() { }              // constructor 1
    complex(float real, float imag)  // constructor 2
    { x = real; y = imag; }
    complex operator+(complex);
    void display(void);
};

complex complex :: operator+(complex c)
{
    complex temp;               // temporary
    temp.x = x + c.x;           // these are
    temp.y = y + c.y;           // float additions
    return(temp);
}

void complex :: display(void)
{
    cout << x << " + j" << y << "\n";

}
```

```
}

int main()
{
    complex C1, C2, C3;          // invokes constructor 1
    C1 = complex(2.5, 3.5);      // invokes constructor 2
    C2 = complex(1.6, 2.7);
    C3 = C1 + C2;

    cout << "C1 = "; C1.display();
    cout << "C2 = "; C2.display();
    cout << "C3 = "; C3.display();

    return 0;
}
```

PROGRAM 7.2

The output of Program 7.2 would be:

```
C1 = 2.5 + j3.5
C2 = 1.6 + j2.7
C3 = 4.1 + j6.2
```

note

> Let us have a close look at the function operator+() and see how the operator overloading is implemented.

```
complex complex :: operator+(complex c)
{
    complex temp;
    temp.x = x + c.x;
    temp.y = y + c.y;
    return(temp);
}
```

We should note the following features of this function:

+   1. It receives only one complex type argument explicitly.
+   2. It returns a complex type value.
+   3. It is a member function of complex.

The function is expected to add two complex values and return a complex value as the result but receives only one value as argument. Where does the other value come from? Now let us look at the statement that invokes this function:

```
C3 = C1 + C2;          // invokes operator+() function
```
