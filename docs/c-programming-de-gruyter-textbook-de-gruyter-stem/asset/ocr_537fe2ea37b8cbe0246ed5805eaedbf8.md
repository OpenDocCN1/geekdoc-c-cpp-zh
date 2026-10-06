# 3.4 Function Overloading

ters and the same types of parameters (no matter what their return types are), the compiler will count it as a compiling error (function redefinition). For example:

+   2. int add(int x, int y);
   void add(int x, int y); //Error: compiler doesn't discriminate
   //functions by their return types

Do not use functions of different functionalities with the same name, as in case any misunderstanding or confusion of the calling result may occur.

```
int add(int x, int y) { return x+y; }
float add(float x, float y) { return x-y; }
```

Here let us see an example of function overloading.

**Example 3.16:** An example of function overloading.
Write three overloaded functions with the same name add, and make them implement the following operations respectively – the addition of two integers, the addition of two real numbers, and the addition of two complex numbers.

Source code:

```
//3_16.cpp
#include<iostream>
using namespace std;
struct complex {
    double real;
    double imaginary;
};
int main() {
    int m, n;
    double x, y;
    complex c1, c2, c3;
    add(int m, int n);
    double add(double x, double y);
    complex add(complex c1, complex c2);

    cout<<"Enter two integer: ";
    cin>>m>>n;
    cout<<"integer "<<m<<'''+<<n<<"="<<add(m,n)<<endl;
```