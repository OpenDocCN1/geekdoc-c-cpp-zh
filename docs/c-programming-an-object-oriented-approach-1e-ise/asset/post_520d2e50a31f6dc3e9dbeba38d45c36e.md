
## 13.6.1 Fraction Class with Overloaded Operators

We created a Fraction class in Chapter 7. In this section we show how we can overload several operators for this class.

## Interface File

Program 13.10 shows the interface file.

### Program 13.10  File fraction.h

```cpp
/***************************************************************
 * The interface file for the Fraction file                    *
 ***************************************************************/
#ifndef Fraction_H
#define Fraction_H
#include <iostream>
#include <cassert>
#include <iomanip>
#include <cmath>
using namespace std;

// Fraction class definition
class Fraction
{
private:
    int numer;
    int denom;
    int gcd (int n, int m = 1);  // Helper function
    void normalize();            // Helper function
public:
    Fraction (int num, int denom);   // Parameter constructor
    Fraction (double value);         // Parameter constructor
    Fraction ();                     // Default constructor
    Fraction (const Fraction& fract); // Copy constructor
    ~Fraction ();                    // Destructor
    // Member operators
    operator double ();              // Conversion
    const Fraction operator+() const;   // Unary plus
    const Fraction operator-() const;   // Unary minus
    Fraction& operator++ ();           // Prefix increment
    Fraction& operator-- ();           // Prefix decrement
    const Fraction operator++ (int);   // Postfix increment
    const Fraction operator-- (int);   // Postfix decrement
    Fraction& operator= (const Fraction& right);  // Assign
    Fraction& operator+= (const Fraction& right); // Compound Assign
    Fraction& operator-= (const Fraction& right); // Compound Assign
    Fraction& operator*= (const Fraction& right); // Compound Assign
    Fraction& operator/= (const Fraction& right); // Compound Assign
```

### Program 13.11  File fraction.cpp (Continued)

```cpp
10    normalize ();
11 }
12 // Parameter Constructor
13 Fraction::Fraction (double value)
14 {
15    denom = 1;
16    while ((value - static_cast<int> (value)) > 0.0)
17    {
18        value *= 10.0;
19        denom *= 10;
20    }
21    numer = static_cast<int> (value);
22    normalize ();
23 }
24 // Default Constructor
25 Fraction::Fraction ()
26 : numer (0), denom (1)
27 {
28 }
29 // Copy Constructor
30 Fraction::Fraction (const Fraction& fract)
31 : numer (fract.numer), denom (fract.denom)
32 {
33 }
34 // Destructor
35 Fraction::~Fraction ()
36 {
37 }
38 // Conversion operator
39 Fraction::operator double ()
40 {
41    double num = static_cast<double> (numer);
42    return (num / denom);
43 }
44 // Unary plus operator
45 const Fraction Fraction::operator+ () const
46 {
47    Fraction temp (+numer, denom);
48    return temp;
49 }
50 // Unary minus operator
51 const Fraction Fraction::operator- () const
52 {
53  Fraction temp(-numer, denom);
54  return temp;
55  }
56  // Pre-increment operator
57  Fraction& Fraction :: operator++ ()
58  {
59      numer = numer + denom;
60      this -> normalize ();
61      return *this;
62  }
63  // Pre-decrement operator
64  Fraction& Fraction :: operator-- ()
65  {
66      numer = numer - denom;
67      this -> normalize ();
68      return *this;
69  }
70  // Post-increment operator
71  const Fraction Fraction :: operator++ (int)
72  {
73      Fraction temp (numer, denom);
74      ++(*this);
75      return temp;
76  }
77  // Post-decrement operator
78  const Fraction Fraction :: operator-- (int)
79  {
80      Fraction temp (numer, denom);
81      --(*this);
82      return temp;
83  }
84  // Assignment operator
85  Fraction& Fraction :: operator= (const Fraction& right)
86  {
87      if (*this != right)
88      {
89          numer = right.numer;
90          denom = right.denom;
91      }
92      return *this;
93  }
94  // Compound Assignment operator (+=)
95  Fraction& Fraction :: operator+= (const Fraction& right)
96 {
97   numer = numer * right.denom + denom * right.numer;
98   denom = denom * right.denom;
99   normalize();
100   return *this;
101 }
102 // Compound Assignment operator (-=)
103 Fraction& Fraction::operator-=(const Fraction& right)
104 {
105   numer = numer * right.denom - denom * right.numer;
106   denom = denom * right.denom;
107   normalize();
108   return *this;
109 }
110 // Compound Assignment operator (*=)
111 Fraction& Fraction::operator*=(const Fraction& right)
112 {
113   numer = numer * right.numer;
114   denom = denom * right.denom;
115   normalize();
116   return *this;
117 }
118 // Compound Assignment operator (/=)
119 Fraction& Fraction::operator/=(const Fraction& right)
120 {
121   numer = numer * right.denom;
122   denom = denom * right.numer;
123   normalize();
124   return *this;
125 }
126 // Addition operator (friend)
127 const Fraction operator+(const Fraction& left, const Fraction& right)
128 {
129   int newNumer = left.numer * right.denom + right.numer * left.denom;
130   int newDenom = left.denom * right.denom;
131   Fraction result (newNumer, newDenom);
132   return result;
133 }
134 // Subtraction operator (friend)
135 const Fraction operator-(const Fraction& left, const Fraction& right)
136 {
137   int newNumer = left.numer * right.denom - right.numer * left.denom;
138   int newDenom = left.denom * right.denom;
139   Fraction result (newNumer, newDenom);
140   return result;
}
// Multiplication operator (friend)
const Fraction operator* (const Fraction& left, const Fraction& right)
{
    int newNumer = left.numer * right.numer;
    int newDenom = left.denom * right.denom;
    Fraction result (newNumer, newDenom);
    return result;
}
// Division operator (friend)
const Fraction operator/ (const Fraction& left, const Fraction& right)
{
    int newNumer = left.numer * right.denom;
    int newDenom = left.denom * right.numer;
    Fraction result (newNumer, newDenom);
    return result;
}
// Equality operator (friend)
bool operator== (const Fraction& left, const Fraction& right)
{
    return (left.numer * right.denom == right.numer * left.denom);
}
// Inequality operator (friend)
bool operator!= (const Fraction& left, const Fraction& right)
{
    return (left.numer * right.denom != right.numer * left.denom);
}
// Less-than operator (friend)
bool operator< (const Fraction& left, const Fraction& right)
{
    return (left.numer * right.denom < right.numer * left.denom);
}
// Less-than or equal operator (friend)
bool operator<= (const Fraction& left, const Fraction& right)
{
    return (left.numer * right.denom <= right.numer * left.denom);
}
// Greater-than operator (friend)
bool operator> (const Fraction& left, const Fraction& right)
{
    return (left.numer * right.denom > right.numer * left.denom);
}
// Greater-than or equal operator (friend)
bool operator>= (const Fraction& left, const Fraction& right)
{
    return (left.numer * right.denom >= right.numer * left.denom);
}
// Extraction operator (friend)
istream& operator >> (istream& left, Fraction& right)
{
    cout << "Enter the value of numerator: ";
    left >> right.numer;
    cout << "Enter the value of denominator: ";
    left >> right.denom;
    right.normalize();
    return left;
}
// Insertion operator (friend)
ostream& operator << (ostream& left, const Fraction& right)
{
    left << right.numer << "/" << right.denom;
    return left;
}
// Helper function (greatest common divisor)
int Fraction::gcd (int n, int m)
{
    int gcd = 1;
    for (int k = 1; k <= n && k <= m; k++)
    {
        if (n % k == 0 && m % k == 0)
        {
            gcd = k;
        }
    }
    return gcd;
}
// Helper function (normalizing a fraction)
void Fraction::normalize ()
{
    if (denom == 0)
    {
        cout << "Invalid denominator in fraction. Need to quit." << endl;
        assert (false);
    }
    if (denom < 0)
    {
```
