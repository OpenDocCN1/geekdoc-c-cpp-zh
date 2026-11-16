
The approach here is similar to overloading the + operator in our previous program with one main difference, the return value. Here we return an int value. Previously we returned an object of class String or an object of class Distance.

## Overloading the Insertion << and Extraction >> Operators

Normally, input and output streams handle only simple data types (int, long, float, double, char*, etc). By overloading the iostream input and output stream operators (>>, <<) you can easily add your own classes to the data types that I/O stream statements are designed to use.

For example, we can treat I/O for user-defined data types in the same way as built-in data types. This is a powerful feature of C++. It lets you say:

```
MyClass foo;
cout << foo;
```

The operator<<() function has already been overloaded for the iostream class, but you can easily overload it for your new class. Let's overload the insertion and extraction operators for the Distance class.

```
class Distance {
private:
    int feet;
    float inches;
public:
    Distance() { feet = 0; inches = 0; }
    Distance(int ft, float in) {
        feet = ft;
        inches = in;
    }
    friend istream& operator>>(istream& is, Distance& d);
    friend ostream& operator<<(ostream& os, const Distance& d);
};

istream& operator>>(istream& is, Distance& d) {
    cout << "Enter feet: "; is >> d.feet;
    cout << "Enter inches: "; is >> d.inches;
    return is;
}

ostream& operator<<(ostream& os, const Distance& d) {
    os << d.feet << "\'" << d.inches << "\'";
    return os;
}
```

```
int main() {
    Distance d1, d2;
    cout << "Enter two Distance values: ";
    cin >> d1 >> d2;
    Distance d3(11, 6.25);
    cout << "d1 = " << d1 << endl;
    cout << "d2 = " << d2 << endl;
    cout << "d3 = " << d3 << endl;
    return 0;
}
```

This program asks for two distance values from the user, and then prints out these values and another value that was initialized in the program. Note that arguments are passed by reference for efficiency.

The input and output operators require, respectively, an istream and ostream object as their left operand. Both return the object upon which they operate. This allows successive input or output operators to be concatenated.

For example:

```
((((( cout << "d1 = " << d1) << "d2 = ") << d2) << endl);
```

Here, each parenthetical sub-expression returns the ostream object cout which becomes the left operand of the next outermost expression.

Because the design of iostreams, an overloaded operator<<() or operator>>() function must be a friend function and it must take arguments of an istream object (either istream or ostream, depending on the operator) followed by an object of your user-defined type. The function must return the same stream object as it takes as an argument.

Note, it's important that the stream object be passed into and out of the function so you can have expressions of the form:

```
cout << obj1 << obj2;
```

In effect, each object is passed to the stream and then the stream is passed down the line.

Note, why couldn't we define the overloaded operator function as a member function of the `Distance` class? If we did, here would be the declaration of the insertion output operator as a member function of `Distance`:

```
class Distance {
    ...
    ostream& operator<<(ostream&);
    ...
};
```

The left operand of every member function is an object or pointer to an object of its class. This is why the member function instance of the output operator declares only the one `ostream` object. A call of this instance takes the following form:

```
d << cout;
```

It would be very confusing both to the programmer and the human readers of the program to provide this instance. Therefore it's better to use friend functions.

## Updated Distance Class

```
// dist4.h
#ifndef _DIST4_H
#define _DIST4_H
#include <iostream.h>
using namespace std;
class Distance {
private:
    int feet;
    float inches;
    void normalize();
public:
    Distance();
    Distance(float f);
    Distance(int ft, float in);
    Distance operator+=(const Distance&);
    friend Distance operator+(const Distance&, const Distance&);
    friend istream& operator>>(istream&, Distance&);
    friend ostream& operator<<(ostream&, const Distance&);
};
#endif

// dist4.cpp
#include <iostream.h>
#include "dist4.h"
Distance::Distance() {
    feet = 0;
    inches = 0.0;
}
Distance::Distance(float f) {
    feet = int(f);
    inches = 12 * (f - feet);
}
Distance::Distance(int ft, float in) {
    feet = ft;
    inches = in;
    normalize();
}

void Distance::normalize() {
    while(inches >= 12.0) {
        inches -= 12.0;
        feet++;
    }
}

Distance Distance::operator+=(const Distance& d) {
    feet += d.feet;
    inches += d.inches;
    return Distance(feet, inches);
}

Distance operator+(const Distance& d1, const Distance& d2) {
    int ft = d1.feet + d2.feet;
    float in = d1.inches + d2.inches;
    return Distance(ft, in);
}

istream& operator>>(istream& is, Distance& d) {
    cout << "Enter feet: "; is >> d.feet;
    cout << "Enter inches: "; is >> d.inches;
    d.normalize();
    return is;
}

ostream& operator<<(ostream& os, const Distance& d) {
    os << d.feet << "\'" << d.inches << "\"";
    return os;
}
```

```
// distdrv4.cpp
#include <iostream>
#include "dist4.h"
using namespace std;
int main() {
  Distance d1(5, 22), d2(8.25), d3, d4, d5;
  cout << "d1: " << d1 << endl;
  cout << "d2: " << d2 << endl;
  cout << "d3: " << d3 << endl;
  cout << "d4: " << d4 << endl;
  cout << "d5: " << d5 << endl;
  d3 = d1 + d2;
  cout << "d3 = d1 + d2: " << d3 << endl;
  d4 = d3 + 10;
  cout << "d4 = d3 + 10: " << d4 << endl;
  cin >> d5;
  cout << "d5: " << d5 << endl;
  return 0;
}
// Output
d1: 6' 10"
d2: 8' 3"
d3: 0' 0"
d4: 0' 0"
d5: 0' 0"
d3 = d1 + d2: 15' 1"
d4 = d3 + 10: 25' 1"
Enter feet: 8
Enter inches: 31
d5: 10' 7"
```

## Overloading the Array Subscript Operator []

The subscript operator [] is normally used to index arrays. In fact, the subscript operator is a binary operator that requires two arguments. For example:

```
p = x[i];

[ ] : operator
x : first argument
i : second argument
```

The subscript operator actually performs a useful function, it hides pointer arithmetic for us! For example, if we have the following array:

```
char name[20];
```

and we execute a statement such as:

```
ch = name[12];
```

The [] operator directs the assignment statement to add 12 to the base address of the array name to locate the data stored in this memory location.

```
ch = name[12] implements pointer arithmetic: *(name + 12)
```

You can overload the array subscript operator [] to provide array-like access to a class's data members, even though that data might be stored as individual members.

Let's overload the [] operator for a class that stores four integer values as separate data members.

```
// parray.h

#ifndef __PARRAY_H
#define __PARRAY_H

class PseudoArray {
private:
    int value0, value1, value2, value3;
public:
    PseudoArray(int v0, int v1, int v2, int v3);
    int getInt(int i);
    int operator[](int i);
};

#endif
```

```
// parray.cpp

#include "parray.h"

PseudoArray::PseudoArray(int v0, int v1, int v2, int v3) {
    value0 = v0;
    value1 = v1;
    value2 = v2;
    value3 = v3;
}

int PseudoArray::getInt(int i) {
    switch(i) {
        case 0 : return value0;
        case 1 : return value1;
        case 2 : return value2;
        case 3 : return value3;
        default: return value0;
    }
}

int PseudoArray::operator[](int i) {
    return getInt(i);
}
```

```
// parraydr.cpp

#include <iostream>
#include "parray.h"

using namespace std;

int main()
{
    PseudoArray pa(10, 20, 30, 40);

    for (int i = 0; i < 4; i++)
        cout << "pa[" << i << "] == " << pa[i] << endl;

    return 0;
}

// parray output

pa[0] == 10
pa[1] == 20
pa[2] == 30
pa[3] == 40
```

To get a data element we might have previously said:

```
cout << pa.getInt(i);
```

We can now say:

```
cout << pa[i];
```

We are using object pa as if it were an array! Overloading the subscript operator makes it possible to use array indexing rather than call member functions for an object of a class.

The overloaded subscript operator function can only be a class member:

```
pa[i] -> pa.operator[](i)
