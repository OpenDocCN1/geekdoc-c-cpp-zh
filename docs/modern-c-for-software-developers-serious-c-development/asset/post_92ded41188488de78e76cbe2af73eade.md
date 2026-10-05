
```cpp
int main()
{
  Foo ob;
  ob.seti(1900);
  cout << ob.get() << endl; // compiler error

  return 0;
}
```

This program will not compile because seti() is declared as const. This means that it is not allowed to modify the data member i. Since seti() attempts to change i, the program fails with a compiler error.

A const member function may not call a non-const member function, since the latter mutate a class data member.

# Overloading Functions With const Reference Parameters

A class can contain two member functions that have identical parameter types and only differ in one of these functions has a const parameter:

```cpp
void set_name(const std::string name);
void set_name(std::string name);
```

The compiler can distinguish between these two member functions on the basis of whether a const or non-const argument is received.

The following program shows this:

```cpp
#include <string>
#include <iostream>

class Dog {
public:
  void set_name(std::string& nm) {
    std::cout << "function called with " + nm << std::endl;
  }
};
```

```cpp
void set_name(const std::string& nm) {
  std::cout << "function called with const parameter: ";
  std::cout << nm << std::endl;
}
```

```cpp
int main() {
  std::string name1("rover");
  std::string name2("fido");
  Dog d;

  d.set_name(name1);
  d.set_name(name2);

  return 0;
}
```

// output
function called with const parameter: rover
function called with fido

# Const Classes

Consider a class which is defined as a const class. A const class can only call const member functions. The syntax for a const class definition is:

```cpp
const class Foo;
```

As the following example shows, foo must only call const functions in a const class. The called functions must be declared as a const functions. The compiler will throw an error if an attempt is made to call a non-const function:

```cpp
#include <string>
#include <iostream>

class Dog {
public:
  void print_name(const std::string name) const { std::cout << "const function called: ";
```

```cpp
std::cout<< name << std::endl;

void print_name(std::string name) { std::cout << "non-const function called: ";
std::cout << name << std::endl; }

int main() {
  class Foo foo;
  foo.print_name("fido");
  
  const class Foo g;
  g.print_name("rover");

  return 0;
}
```

Output
non-const function called: fido
const function called: rover

# Mutable Data Members

Sometimes there are one or more data members of a class that we want a const function to be able to modify, even though we don't want the function to be able to modify any other data members. We can implement this by declaring these data members to be **mutable**. A mutable data member can be modified by a const function.

```cpp
#include <iostream>
class Foo {
  mutable int i;
  public:
  Foo() { i = 0; }

  int geti() const {
    return i; // OK
  }

  void seti(int x) const {
    i = x; // OK since i is mutable
  }
}
```

```cpp
int main()
{
    Foo obj;
    obj.seti(5);
    std::cout << obj.get() << std::endl;
}
// output
5
```

# Why Using const Is Important

const correctness is a powerful technique for writing better and safer C++ code. The use of const can avoid a lot of trouble and debugging time because violations of const cause compile-time errors. In addition, using const enables the compiler to perform more optimizations.

Principle: Pay attention to const-correctness and use const whenever possible.

# Volatile Variables

The volatile keyword informs the compiler that a variable may change without the program knowing about the change. Variables that are declared as volatile will not be cached by the compiler.

# Volatile Member Functions

Class member functions can be declared as volatile. This causes the this pointer to be treated as a volatile pointer (the pointer can change without the program knowing about the change). The syntax for a volatile member function is:

```cpp
class X {
public:
    void f2(int a) volatile; // declare volatile member function
}
```

# C++ Copy Constructors

By default, C++ performs a bitwise copy during an object assignment such as Foo = Bar. That is, an identical copy of the object is made. Although this is perfectly adequate for many cases and exactly what we want to happen, there are situations in which a bitwise copy must not be used. One of the most common cases is when an object allocates memory when it is created. For example, assume we have a class MyClass that allocates memory whenever an instance is created. Let A be an instance of this class and suppose that we have the following assignment:

```cpp
MyClass B = A;
```

If a bitwise copy is performed, then B will be an exact copy of A. This means that B will be using the same piece of allocated memory that A is using, instead of allocating its own memory. Clearly, this is dangerous. For example, if MyClass includes a destructor that frees allocated memory, then the same piece of memory will be freed twice when A and B are destroyed.

C++ solves this problem with copy constructors. A copy constructor initializes an object using another object.

The syntax for a copy constructor is:

```cpp
ClassName(const ClassName& obj) {
  // body of constructor
}
```

obj is a reference to an object of type ClassName. It is permissible for a copy constructor to have additional parameters. However, in all cases, the first parameter must be a reference to the object that will be used to initialize the new object.

Note: If the ampersand & is omitted in the copy constructor, the constructor will do a bitwise copy.

It is important to understand that C++ defines two distinct types of situations in which the value of one object is given to another. The first is assignment. The second is initialization. Initialization can occur in any of the following three ways:

- when one object explicitly initializes another in a declaration.
- when a copy of an object is made during a function call.
- when an object receives a function return value

The copy constructor applies only to initializations. It does not apply to assignments. For example, assume that we have a class Foo, and that foo is an object of this class, each of the following statements involves initialization:

- Foo foo(x) // constructor invoked with argument x
- Foo foo = 5; // constructor has one scalar parameter
- func(foo) // foo passed as a function argument
- foo = func(); // foo receives a temporary return value

The following example shows two ways to create an object that wraps an array:

```cpp
#include <iostream>
#include <new>
#include <cstdlib>
using namespace std;

class Foo
{
    int *p;
    int size;
public:
    // constructor
```

```cpp
Foo(int sz) {
try {
    p = new int[sz];
} catch (bad_alloc& err) {
    cout << "Allocation Failure\n";
    exit(1);
}

    size = sz;
}
```

```cpp
~Foo() { delete [] p; }
```

```cpp
~Foo() { delete [] p; }
```

```cpp
// copy constructor
Foo(Foo& a) {
void put(int i, int j) {
    if(i >= 0 && i < size) p[i] = j;
}

int get(int i) { return p[i]; }
int get_size() { return size; }
}
```

```cpp
// Copy Constructor
Foo(Foo& a) {
int i;
int sz = a.get_size();
try {
    p = new int[sz];
} catch (bad_alloc& err) {
    cout << "Allocation Failure\n";
    exit(1);
}

for(i = 0; i < size; i++) p[i] = a.get(i);
}
```

```cpp
int main() {
Foo numarray(10);
int i;
for(i = 0; i < 10; i++) numarray.put(i, i);
for(i = 9; i >= 0; i--) cout << numarray.get(i) << "", ";
cout << endl;
}
```

```cpp
// copy constructor invoked
Foo(numarray);
for(i = 0; i < 10; i++) cout << foo.get(i) << "", ";
}
```

```cpp
// output
9, 8, 7, 6, 5, 4, 3, 2, 1, 0,
0, 1, 2, 3, 4, 5, 6, 7, 8, 9,
```

When foo object is created by invoking the copy constructor, memory for the new array is allocated and the array in numarray is copied to foo's array. In this way, foo and numarray have arrays that contain the same values, but each array is separate and distinct. (That is, numarray::p and foo::p do not point to the same location in memory.)

If the copy constructor had not been used, the default bitwise initialization would have resulted in foo and numarray sharing the same memory for their arrays. (That is, numarray::p and foo::p would have pointed to the same location.)

The copy constructor is only called to initialize an object. For example, the following code does not call the copy constructor defined in the preceding program:

```cpp
Foo foo;

Foo bar;

// does not invoke the copy constructor
// this is a copy assignment
foo = bar;
```
