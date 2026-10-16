
We know that a member function can be invoked only by an object of the same class. Here, the object C1 takes the responsibility of invoking the function and C2 plays the role of an argument that is passed to the function. The above invocation statement is equivalent to

```
C3 = C1.operator+(C2);    // usual function call syntax
```

Therefore, in the operator+() function, the data members of C1 are accessed directly and the data members of C2 (that is passed as an argument) are accessed using the dot operator. Thus, both the objects are available for the function. For example, in the statement

```
temp.x = x + c.x;
```

c.x refers to the object C2 and x refers to the object C1. temp.x is the real part of temp that has been created specially to hold the results of addition of C1 and C2. The function returns the complex temp to be assigned to C3. Figure 7.1 shows how this is implemented.

As a rule, in overloading of binary operators, the left-hand operand is used to invoke the operator function and the right-hand operand is passed as an argument.

![](img/58ab8f034e2127e80560390a921c2523_183_0.png)

Fig. 7.1 ⇔ Implementation of the overloaded + operator

We can avoid the creation of the temp object by replacing the entire function body by the following statement:

```
return complex((x+c.x),(y+c.y));    // invokes constructor 2
```

What does it mean when we use a class name with an argument list? When the compiler comes across a statement like this, it invokes an appropriate constructor, initializes an object with no name and returns the contents for copying into an object. Such an object is called a temporary object and goes out of space as soon as the contents are assigned to another object. Using *temporary objects* can make the code shorter, more efficient and better to read.

## 7.5 Overloading Binary Operators Using Friends

As stated earlier, friend functions may be used in the place of member functions for overloading a binary operator, the only difference being that a friend function requires two arguments to be explicitly passed to it, while a member function requires only one.

The complex number program discussed in the previous section can be modified using a friend operator function as follows:

- 1. Replace the member function declaration by the friend function declaration.
  
      ```cpp
      friend complex operator+(complex, complex);
      ```
  
- 2. Redefine the operator function as follows:
  
      ```cpp
      complex operator+(complex a, complex b)
      {
          return complex((a.x+b.x),(a.y+b.y));
      }
      ```

In this case, the statement

```
C3 = C1 + C2;
```

is equivalent to

```
C3 = operator+(C1, C2);
```

In most cases, we will get the same results by the use of either a friend function or a member function. Why then an alternative is made available? There are certain situations where we would like to use a friend function rather than a member function. For instance, consider a situation where we need to use two different types of operands for a binary operator, say, one an object and another a built-in type data as shown below,

```
A = B + 2;  (or A = B + 2;)
```

where A and B are objects of the same class. This will work for a member function but the statement

```
A = 2 + B; (or A = 2 * B)
```

will not work. This is because the left-hand operand which is responsible for invoking the member function should be an object of the same class. However friend function allows both approaches. How?

It may be recalled that an object need not be used to invoke a friend function but can be passed as an argument. Thus, we can use a friend function with a built-in type data as the left-hand operand and an object as the right-hand operand. Program 7.3 illustrates this, using scalar multiplication of a vector. It also shows how to overload the input and output operators >> and <<.

## OVERLOADING OPERATORS USING FRIENDS

```
#include <iostream.h>

const size = 3;

class vector
{
    int v[size];
public:
    vector();                         // constructs null vector
    vector(int *x);                   // constructs vector from array
    friend vector operator *(int a, vector b);      // friend 1
    friend vector operator *(vector b, int a);      // friend 2
    friend istream & operator >> (istream &, vector &);
    friend ostream & operator << (ostream &, vector &);
};

vector :: vector()
{
    for(int i=0; i<size; i++)
        v[i] = 0;
}

vector :: vector(int *x)
{
    for(int i=0; i<size; i++)
        v[i] = x[i];
}
```

```
vector operator *(int a, vector b)
{
    vector c;

    for(int i=0; i < size; i++)
        c.v[i] = a * b.v[i];
    return c;
}

vector operator *(vector b, int a)
{
    vector c;

    for(int i=0; i<size; i++)
        c.v[i] = b.v[i] * a;
    return c;
}

istream & operator >> (istream &din, vector &b)
{
    for(int i=0; i<size; i++)
        din >> b.v[i];
    return(din);
}
ostream & operator << (ostream &dout, vector &b)
{
    dout << "(" << b.v [0];
    for(int i=1; i<size; i++)
        dout << ", " << b.v[i];
    dout << ")";
    return(dout);
}

int x[size] = {2,4,6};

int main()
{
    vector m;            // invokes constructor 1
    vector n = x;        // invokes constructor 2

    cout << "Enter elements of vector m " << "\n";
    cin >> m;            // invokes operator>>() function
```

```
cout << "\n";
cout << "m = " << m << "\n";        // invokes operator <<()

vector p, q;

p = 2 * m;                // invokes friend 1
q = n * 2;                // invokes friend 2

cout << "\n";
cout << "p = " << p << "\n";        // invokes operator<<()
cout << "q = " << q << "\n";

return 0;
}
```

PROGRAM 7.3

Shown below is the output of Program 7.3:

```
Enter elements of vector m
5 10 15

m = (5, 10, 15)
p = (10, 20, 30)
q = (4, 8, 12)
```

The program overloads the operator * two times, thus overloading the operator function operator*() itself. In both the cases, the functions are explicitly passed two arguments and they are invoked like any other overloaded function, based on the types of its arguments. This enables us to use both the forms of scalar multiplication such as

```
p = 2 * m;        // equivalent to p = operator*(2,m);
q = n * 2;        // equivalent to q = operator*(n,2);
```

The program and its output are largely self-explanatory. The first constructor

```
vector();
```

constructs a vector whose elements are all zero. Thus

```
vector m;
```

creates a vector m and initializes all its elements to 0. The second constructor

```
vector(int &x);
```

```
int x[3] = {2, 4, 6};
vector n = x;
```

create n as a vector with components 2, 4, and 6.

note
We have used vector variables like m and n in input and output statements just like simple variables. This has been made possible by overloading the operators >> and << using the functions:

friend istream & operator>>(istream &, vector &);
friend ostream & operator<<(ostream &, vector &);

istream and ostream are classes defined in the iostream.h file which has been included in the program.

## 7.6 Manipulation of Strings Using Operators

ANSI C implements strings using character arrays, pointers and string functions. There are no operators for manipulating the strings. One of the main drawbacks of string manipulations in C is that whenever a string is to be copied, the programmer must first determine its length and allocate the required amount of memory.

Although these limitations exist in C++ as well, it permits us to create our own definitions of operators that can be used to manipulate the strings very much similar to the decimal numbers. (Recently, ANSI C++ committee has added a new class called string to the C++ class library that supports all kinds of string manipulations. String manipulations using the string class are discussed in Chapter 15.

For example, we shall be able to use statements like

```
string3 = string1 + string2;
if(string1 >= string2) string = string1;
```

Strings can be defined as class objects which can be then manipulated like the built-in types. Since the strings vary greatly in size, we use new to allocate memory for each string and a pointer variable to point to the string array. Thus we must create string objects that can hold these two pieces of information, namely, length and location which are necessary for string manipulations. A typical string class will look as follows:

```
class string
{
    char *p;        // pointer to string
```
