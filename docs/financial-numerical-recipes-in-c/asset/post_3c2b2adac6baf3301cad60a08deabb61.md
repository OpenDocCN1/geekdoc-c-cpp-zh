
## 1.2.3 Functions and libraries

In addition to the basic mathematical operations there is a large number of additional operations that can be performed on any type. However, these are not parts of the core language, they are implemented as standalone functions (most of which are actually written in C or C++). These functions are included in the large library that comes with any C++ installation. Since they are not part of the core language they must be defined to the compiler before they can be used. Such definitions are performed by means of the include statement.

For example, the mathematical operations of taking powers and performing exponentiation are defined in the mathematical library cmath. In the C++ program one will write

```
#include <cmath>
```

cmath is actually a file with a large number of function definitions, among which one finds pow(x,n) which calculates x^n, and exp(r) which calculates e^r. The following programming stub calculates a = 2^2 and b = e^1.

```
#include <cmath>
double a = pow(2,2);
double b = exp(1);
```

which will give the variables a and b values of 4 and 2.718281828..., respectively.

## 1.2.4 Templates and libraries

The use of libraries is not only limited to functions. Also included in the standard library is generic data structures, which can be used on any data type. The example we will be considering the most is the vector<>, which defines an array, or vector of variables.

```
#include <vector>
vector<double> M(2);
M[0]=1.0;
M[1]=2.0;
M.push_back(3);
```

This example defines an array with three elements of type double

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_7_0.png)

Note some peculiarities here. When first defining the vector with the statement

```
vector<double> M(2);
```

we defined an array of 2 elements of type double, which we then proceeded to fill with the values 1 and 2. When filling the array we addressed each element directly. Note that in the statement

```
M[0]=1.0;
```

lies one of the prime traps for programmers coming to C or C++ from another language. Indexing of arrays starts at zero, not at one. M[0] really means the first element of the array.

The last statement,

```
M.push_back(3);
```

shows the ability of the programmer of changing the size of the array after it has been defined. push_back is a standard operation on arrays which "pushes" the element onto the back of the array, extending the size of the array by one element. Most programming languages do not allow the programmer to specify variable-sized arrays "on the fly". In FORTRAN or Pascal we would usually have to set a maximum length for each array, and hope that we would not need to exceed that length. The vector<> template of C++ gets rid of the programmers need for "bookkeeping" in such array manipulations.

## 1.2.5 Flow control

To repeat statements several times one will use one of the possibilities for flow control, such as the for or while constructs. For example, to repeat an operation n times one can use the following for loop:

```
for (int i=0; i<n; i++) {
    some_operation(i);
};
```

The for statement has three parts. The first part gives the initial condition (i=0). The next part the terminal condition (i<n), which says to stop when i<n is not fulfilled, which is at the n'th iteration. The last part is the increment statement (i++), saying what to do in each iteration. In this case the value of i is increased by one in each iteration. This is the typical for statement. One of the causes of C's reputation for terseness is the possibility of elaborate for constructs, which end up being almost impossible to read. In the algorithms presented in this book we will try to avoid any obfuscated for statements, and stick to the basic cases.

## 1.2.6 Input Output

For any program to do anything useful it needs to be able to output its results. Input and output operations is defined in a couple of libraries, iostream and fstream. The first covers in/output to standard terminals and the second in/output to files.

To write to standard output cout (the terminal), one will do as follows:

```
#include <iostream>
cout << "This is a test" << endl;
```

To write to a file "test.out", one will do as follows:

```
#include <fstream>
ofstream outf;
outf.open("test.out");
outf << "This is a test" << endl;
outf.clear();
outf.close();
```

## 1.2.7 Splitting up a program

Any nontrivial program in C++ is split into several pieces. Usually each piece is written as a function which returns a value of a given type. To illustrate we provide a complete example program, shown in C++ Code 1.1.

```
#include <iostream> // input output operations
#include <cmath> // mathematics library
using namespace std; // the above is part of the standard namespace
double power(double x, double n)
{
    // define a simple power function
    double p = exp(n*log(x));
    return p;
};
int main(){
    for (int n=1;n<6;n++){
        cout << " 2^" << n << " = " << power(2,n) << endl;
    }
};
```

C++ Code 1.1: A complete program

The program defines a function performing the mathematical power operation, power(x, n) which calculates x^n through the identity x^n = e^{n ln(x)}. This function is then used to calculate and print the first 5 powers of 2.

When compiled, linked and run, the program will provide the following output

2^1 = 2
2^2 = 4
2^3 = 8
2^4 = 16
2^5 = 32

## 1.2.8 Namespaces

To help in building large programs, the concept of a namespace was introduced. Namespaces are a means of keeping the variables and functions defined local to the context in which they are used. For now it is necessary to know that any function in the standard C++ library lies in its own namespace, called the standard namespace. To actually access these library functions it is necessary to explicitly specify that one wants to access the standard namespace, by the statement

```
using namespace std;
```

Instead of such a general approach, one can also specify the namespace on an element by element basis, but this is more a topic for specialized C++ texts, for the current purposes we will allow all routines access to the whole standard namespace.

## 1.3 Extending the language, the class concept.

One of the major advances of C++ relative to other programming languages is the programmers ability to extend the language by creating new data types and defining standard operations on these data types. This ability is why C++ is called an object oriented programming language, since much of the work in programming is done by creating objects. An object is best thought of as a data structure with operations on it defined. How one uses an object is best shown by an example.

## 1.3.1 date, an example class

Consider the abstract concept of a date. A date can be specified in any number of ways. Let us limit ourselves to the Gregorian calendar. 12 august 2003 is a common way of specifying a date. However, it can also be represented by the strings: "2003/8/12", "12/8/2003" and so on, or by the number of years since 1 january 1900, the number of months since January, and the day of the month (which is how a UNIX programmer will think of it).

However, for most people writing programs the representation of a date is not relevant, they want to be able to enter dates in some abstract way, and then are concerned with such questions as:

- Are two dates equal?
- Is one date earlier than another?
- How many days is it between two dates?

A C++ programmer will proceed to use a class that embodies these uses of the concept of a date. Typically one will look around for an extant class which has already implemented this, but we will show a trivial such date class as an example of how one can create a class.

```
class date {
protected:
    int year_;
    int month_;
    int day_;
public:
    date();
    date(const int& d, const int& m, const int& y);
    bool valid() const;
    int day() const;
    int month() const;
    int year() const;
    void set_day (const int& day );
    void set_month( const int& month );
    void set_year( const int& year );
    date operator ++(); // prefix
    date operator ++(int); // postfix
    date operator --(); // prefix
    date operator --(int); // postfix
};

bool operator == (const date&, const date&); // comparison operators
bool operator != (const date&, const date&);
bool operator < (const date&, const date&);
bool operator > (const date&, const date&);
bool operator <= (const date&, const date&);
bool operator >= (const date&, const date&);
```

## Header file 1.1: Defining a date class

A class is defined in a header file, as shown in Header file 1.1. As internal representation of the date is chosen the three integers day_, month_ and year_. This is the data structure which is then manipulated by the various functions defined below.

The functions are used to
