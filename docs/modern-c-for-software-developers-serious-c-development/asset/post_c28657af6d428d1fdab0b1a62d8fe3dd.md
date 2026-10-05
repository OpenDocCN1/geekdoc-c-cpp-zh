
memory location with a 5 value will not exist after the statement has finished executing.

The following shows examples of manipulating independent reference variables:

```cpp
#include <iostream>
int main() {
    int a = 10;
    // independent reference to a
    int &r = a;

    // a and r have the same values
    std::cout << "a: " << a << " ref: " << r << "\n";

    // changing the value of r changes
    r = 100;
    std::cout << "a: " << a << " ref: " << r << "\n";

    // put variable b's value in r
    int b = 19;
    r = b;
    std::cout << "b: " << b << " a: " << a << " r: " << r << "\n";

    // decrementing r also decrements b
    r--;
    std::cout << "b: " << b << " r: " << r << "\n";

    // output
    a: 10 r: 10
    a: 100 r: 100
    b: 19 r: 19
    a: 18 r: 18
}
```

## Restrictions On References

A number of restrictions apply to references:

- null references are prohibited (the implicit pointer cannot point to null)
- we cannot reference a reference. Put differently, we cannot obtain the address of a reference.
- we cannot create a pointer to a reference

An independent reference variable must be initialized when it is declared.

## Dangling References

A dangling reference refers to a reference variable that points to a value that does not exist or does not have an addressable memory location. In the example below, the function returns a reference that points to a local value on the stack:

```cpp
#include <iostream>
int& foo() {
    int x = 5;
    return x;
}
int main() {
    int& ret = foo();
    std::cout << ret << std::endl;
}
// error: reference to local variable x returned.
```

This program will not compile. The return value exists on the stack and will cease to exist after the function returns.

## Returning A Const Reference From A Class Member Function

Consider the following program:

```cpp
#include <string>
#include <iostream>
class Dog {
public:
    std::string name;
    Dog(std::string nm) { name = nm; }
    const std::string& get_name() { return name; }
};
```

```cpp
int main()
{
    class Dog d("rover");
    const std::string& dog_name = d.get_name();

    std::cout << dog_name << std::endl;
}
//output
rover
```

The const reference in the Dog::get_name declaration signifies that the value of the reference variable dog_name cannot be changed. Because of this restriction, a statement such as:

d.get_name() = "fido"

will not compile.

## C++ Function Overloading

Function overloading is an example of compile-time polymorphism. Function overloading is the process of using the same function name for two or more functions. In function overloading, each redefinition of a function uses different types of function parameters or a different number of parameters. These differences enables the compiler to know which function to call in any given situation.

Here is an example:

```cpp
#include <iostream>
using namespace std;

// forward declarations
// these functions differ in the types of the parameters
int myfunc(int i);
double myfunc(double i);

int main() {
    cout << myfunc(10) << " "; // calls myfunc(int i)
    cout << myfunc(5.4); // calls myfunc(double i)
    return 0;
}

double myfunc(double i) {
    return i;
}

int myfunc(int i) {
    return i;
}

// output
10 5.4
```

Two functions that differ only in their return types cannot be overloaded.

Sometimes, two function declarations will appear to be different, when in fact they are not. For example:

```cpp
void f(int *p);
void f(int p[]); // error, *p is same as p[]
```

A program containing these declarations will not compile. To the compiler *p is the same as p[].

## Overloading Constructor Functions

There are three main reasons why we will want to overload a constructor: to gain flexibility, to allow both initialized and uninitialized objects to be created, and to define copy constructors.

## Finding the Address of an Overloaded Function

A function name by itself is also the address of a function. One reason that we need function addresses is to assign an address to a function pointer and then call this function through the pointer.

If a function is not overloaded, obtaining a function address is straightforward. However, for overloaded functions, the process is more subtle. To understand why, first consider this statement, which assigns the address of a function called myfunc() to the pointer p:

```cpp
p = myfunc;
```

If myfunc() is not overloaded, there is one and only one function called myfunc, and the compiler has no difficulty assigning its address to p. However, if myfunc() is overloaded, how does the compiler know which function address to assign to p? The answer is that it depends upon how p is declared.

Consider this program:

```cpp
#include <iostream>
using namespace std;

// forward declarations
int myfunc(int a);
int myfunc(int a, int b);

int main() {
    // pointer to a function with declaration int f(int)
    int (*fp)(int);             // points to myfunc
    fp = myfunc;

    cout << fp(5) << endl;

    // pointer to a function with declaration int f(int, int)
    int (*f)(int, int);
    f = myfunc;

    cout << f(5, 6) << endl;
}

int myfunc(int a) {
    return a;
}

int myfunc(int a, int b) {
    return a*b;
}

// output
5
30
```

Here, there are two versions of myfunc(). Both return an int, but one takes a single integer argument and the other requires two integer arguments. In this program, fp is declared as a pointer to a function with declaration int f(int). fp points to myfunc. When fp is assigned the address of myfunc, it selects the myfunc(int) version. If f had been declared as int (*f)(int, int), it would have selected the myfunc(int, int) version.

## Default Arguments

C++ allows a function parameter to be assigned a default value when an argument is not specified. The following example declares foo() as taking one argument with a default value of 0.0:

```cpp
void foo(double d = 0.0)
{
}
```

Now, foo() can be called in any of two ways, as the following examples show:

```cpp
foo(19.234); // pass an explicit value
foo();       // use the default value
```

All parameters that take default values must appear to the right of those that do not. Once we begin the definition of parameters that take default values, we cannot specify a non-defaulting parameter. That is, a declaration like this will not compile:

```cpp
int myfunc(float f, int=10, char *str);
```

It is permissible to use default parameters in an object's constructor.

## Overloading And Implicit Casts

C++ automatically tries to convert the arguments used to call a function into the parameter types expected by the function.

```cpp
int myfunc(double d);

// not an error, implicit conversion applied
cout << myfunc('c');
```

This is not an error because C++ automatically converts the character c into its double equivalent. Type conversions that are not narrowing are always implicitly applied by the compiler when required.

## Const And Mutable Member Functions

## const Member Functions

Class member functions can be declared as const functions. A const function does not modify the data members of the class that it belongs to. A member function that is declared as a const function cannot call a non-const member function.

The syntax for a const member function is:

```cpp
 Foo
{
    int some_var;
    public:
    int func() const; // const member function
};
```

The attribute keyword const is part of the function declaration.

The following example shows a program with const member functions that will not compile:

```cpp
#include <iostream>
using namespace std;
class Foo
{
    int i;
    public:
    int geti() const {
        return i;        // OK
    }
    void seti(int x) const {
        i = x;           // compiler error
    }
};
```
