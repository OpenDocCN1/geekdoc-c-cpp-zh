
# MISCELLANEOUS TOPICS

```cpp
J = j;
}
int getI(){return I;}
int getJ(){return J;}
//void setI(int i){I = i;}
```

```cpp
int main() {
  X x(1, 2);
  cout << x.getI() << " " << x.getJ() << endl;
  x.J = 3;
//x.I = 4;
  return 0;
}
```

The program will print the integers 1 and 2 to standard output. Removal of the comments before the setI function in the X definition will produce a compile error. The value of a const member variable can be set only within a constructor initializer list. Because we are working with a struct, member variables are public by default and their values can be changed. Thus, it is legal to change the value of the J variable from next to last inside main. The same is not true for I and removing the comment from next to last line will also produce a compilation error.

An equivalently constructor for the Class X

```cpp
X(int i, int j) : I(i), J(j) {}
I = i;
J = j;
```

```cpp
//constEx2.cpp
#include <iostream>

using namespace std;
class X{
const int I;
static const int J = 2;

public:
  X(int i) : I(i) {}
  int getI(){return I;}
  int getJ(){return J;}
};
```

```cpp
int main() {
  X x1(1);
  cout << x1.getI() << " " << x1.getJ() << endl;
  X x2(2);
  cout << x2.getI() << " " << x2.getJ() << endl;
  return 0;
}
```

Here the class has static const and const class members. In main instances of the class are created for different values of the const data members and then the values of all variables are written to standard output producing: 

This demonstrates that the value of the static const class member is the same across instances of the class.

We discussed pointers and references earlier in this section. In general, any object can be declared const with the meaning that none of its data members can be modified. To ensure this is the case, ordinary member functions are forbidden from working with const objects. This leads to a member dichotomy where there are ordinary member functions as well as others that are guaranteed not to modify an object's data members. The latter functions are given a special const designation that takes the form

```cpp
returnType functionName(arguments) const {
```

The const keyword is actually a part of the function's signature. Consequently, it must appear in the prototype and definition for the function and one can have overloaded functions with the same name and arguments that differ only in terms of the const modifier. Both the compiler and linker will make sure that only const member functions are called by const objects.

The listing below illustrates the difference between const and non-const member functions.

```cpp
//constEx3.cpp
#include <iostream>

using namespace std;

struct X{
  int I;

  X(int i) : I(i) {}
  int getI() {return I;}
  int getI() const {return I;}
};

int main() {
  X x1(1);
  const X x2(2);
  cout << x1.getI() << endl;
  cout << x1.getI() << endl;
  cout << x2.getI() << endl;
  //cout << x2.getI() << endl;
  return 0;
}
```

# MISCELLANEOUS TOPICS

The X struct has two accessor functions for its I variables: a version with the const designation (i.e., getConst) and one without (getI). This program will compile and run in its current form illustrating that a const member function can be called by either const or non-const objects. However, if the next last line in main is uncommented, the compiler will respond with the admonishment: passing const X as the next of int getI() discards qualifiers.

This refers to the fact that the x2 object is const with the consequence that its pointer becomes a const object. In particular, this entails that it cannot be used with a non-const member function.

A somewhat meaningful example that has implications for developments in Section 3 is provided by the next list. Listing 3.9 constEx4.cpp

```cpp
//constEx4.cpp
#include <iostream>
using namespace std;
struct X{
    int I, J;
public:
    X(int i, int j) : I(i), J(j) {}
    X operator*(int a);
    X operator*(int a) const;
};

X::operator*(int a) {
    cout << "const version of *" << endl;
    return x; // Note: original text might have error here, keeping logic
}
X::operator*(int a) const {
    cout << "const version of *" << endl;
    return x;
}
X::operator*(int a, const& x){
    return x;
}
int main() {
    X x(1, 2);
    cout << (x*2).I << " " << (x*2).J << endl;
    cout << (2*x).I << " " << (2*x).J << endl;
    return 0;
}
```

In this case, the same struct of X as in the previous examples is used that has data members I and J. The difference is that a form of multiplication has been defined for the struct through a process called operator overloading that will now be described.

# SKETCH OF C++

We have already seen that C++ allows function overloading. The same is true for the arithmetic operators as +, /, *, the operators +=, /=, *= and others. To create an overloaded operator use the syntax

```cpp
returnType operatorName(arguments)
```

As a case in point, overloaded versions of the multiplication operator have been defined for the X struct in Listing 3.9: one is designated as const and one is not. Both operators in the X struct work for expressions of the form X*a with an object and an integer. Expressions like a* are problematic; this would only make sense if integers themselves were a case. However, the two-argument version of * directly as an argument should be passed in a const reference to make certain that the const version of * operator in the X class can be used to carry out the computation. The code in Listing 3.9 was compiled and executed to produce:

```
2
const version of *
2
```

The output shows that, as expected, the non-const version of * was used for right-hand multiplication of the X object while the const version was used to carry left multiplication. Actually, the presence of two multiplication operators is redundant here in that the const version can be used exclusively without loss of functionality for the class.

# 3.8.4 Forward references

As programs grow, more complex relationships can develop between different classes. It is commonly the case that objects of one class will produce and operate on objects of another. A simple example of this is provided by the next listing. Listing 3.10 circular

```cpp
//circular.cpp
struct Y;//forward declaration
struct X {
  Y* A;
  X(){}
  X(Y* a){A = a;}
  Y& funcX(Y& y){return y;}
};

struct Y {
  X B;
  Y(){}
  Y(X b){B = b;}
  X funcY(X x){return x;}
}
```

# MISCELLANEOUS TOPICS

```cpp
int main(){
  X x; Y y;
  return 0;
}
```

The initial line of code, `struct Y;`, that appears in Listing 3.10 would seem to be of questionable value and not informative. This type of statement is known as a forward declaration and actually serves an important purpose. It tells the compiler that a struct Y exists that will be defined at a later point. In its present this compiles and executes without a problem. Commenting out the forward declaration will produce a compile error that contains a statement as this:

```
compiler.cpp5: error: ISO C++ forward declaration of 'Y' with no type
```

For the X struct to use Y the compiler simply must know that the Y exists and the forward reference solves this problem. One course, this solution might be to just define the Y first, rather than defining it. But, the Y struct in this case X moves around the "circle" and a forward declaration of the X struct would be required before this alternate arrangement could be operable. There is more going on in Listing 3.10 than just the use of a forward reference. Y objects arise in the X struct in form of pointers or references. If this is changed the case seeing that no details of Y have been supplied when the compiler encounters the definition of the X struct. If an actual Y is to be a member of the X struct or a method or return type, the compiler needs to determine how much memory to allocate or require a priori: namely, the four or eight bytes that is needed to hold an address. For similar reasons, if the Y struct definition were moved ahead of the X struct the resulting code would fail to compile even with the inclusion of a forward reference to the X struct. This happens because Y requires X objects by value. While the positioning of the X and Y objects is somewhat inconvenient here, the problems arise in a more general context can be realized through restructuring the Listing 3.10 into separate files with separate headers. For the X struct we use

```cpp
//x.h
#ifndef X_H
#define X_H
struct Y;
struct X {
  Y* A;
  X(){}
  X(Y* a){A = a;}
  Y& func(Y& y){return y;}
};
#endif
```

while the Y struct has header file

```cpp
//y.h
#ifndef Y_H
#define Y_H
#include "x.h"
```

```cpp
struct Y {
```
