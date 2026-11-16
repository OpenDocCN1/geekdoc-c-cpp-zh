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

# 1.2.8 Namespaces

To help in building large programs, the concept of a namespace was introduced. Namespaces are a means of keeping the variables and functions defined local to the context in which they are used. For now it is necessary to know that any function in the standard C++ library lies in its own namespace, called the standard namespace. To actually access these library functons it is necessary to explicitly specify that one wants to access the standard namespace, by the statement

```
using namespace std;
```

Instead of such a general approach, one can also specify the namespace on an element by element basis, but this is more a topic for specialized C++ texts, for the current purposes we will allow all routines access to the whole standard namespace.

# 1.3 Extending the language, the class concept.

One of the major advances of C++ relative to other programming languages is the programmers ability to extend the language by creating new data types and defining standard operations on these data types. This ability is why C++ is called an object oriented programming language, since much of the work in programming is done by creating objects. An object is best though of as a data structure with operations on it defined. How one uses an object is best shown by an example.