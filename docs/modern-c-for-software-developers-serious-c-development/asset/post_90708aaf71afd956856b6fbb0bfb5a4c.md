
This includes all private elements.

Member data variables in a class declaration have some limitations:

- No member variable can be declared as an extern or register variable.
- A non-static member variable cannot be initialized through an assignment (at the point of it' declaration in the class).

As a general rule, we should enforce encapsulation of data. That is, all of the data members in a class should be declared as private.

## Accessing Public Members

The syntax for accessing a public member is as follows: Specify the object's name, then the dot operator, and then the member variable or member function.

```cpp
#include <iostream>
using namespace std;

class Foo {
public:
    // these data variables are accessible to the entire program
    int i, j, k;
};

int main() {
    Foo a, b;
    // access to i, j, and k is OK
    a.i = 100;
    a.j = 4;
    a.k = a.i * a.j;

    b.k = 12; // different class instance

    cout << a.k << " " << b.k;
    return 0;
}

// output
400 12
```

## The Scope Resolution Operator

The :: scope resolution operator associates a member with a class name. This tells the compiler which class the member belongs to. The scope resolution operator also has another related use: it can allow access to a name within some scope. This allows access to a name in some scope that is identical to a local declaration with the name.

The following example shows how this works:

```cpp
int i;      // global variable i
void f() {
    int i;      // local variable i
    i = 10;     // uses local i
}

void g() {
    int i;      // local variable i
    ::i = 10;    // refers to the global variable i
}
```

## Class Function Implementations

Consider the following class specification:

```cpp
#include <iostream>
#include <cstring>

using namespace std;

class Foo {
public:
    void buildstr(char *s);
    void showstr();

private:
```

```cpp
char str[255];

void Foo::buildstr(char *s) {
  // initialize the member string variable
  strcpy(str, s);
}

void Foo::showstr() {
  cout << str << "\n";
}
```

The class in this example only contains the class member function prototypes. The actual class function implementations follow the class and use the scope resolution operator to identify the class to which each belongs. This is the normal way in which a class is declared. We can however provide function implementations within a class.

## Static Class Members

Member functions and member variables of a class can be declared as static. Static members are shared by all of the instances of a class. The following restrictions apply:

- A static member function may only refer to other static member functions and static data members of the class
- A static member function does not have a this pointer.
- We cannot have a static and non-static version of a member function.
- A static function cannot be declared with a const or volatile attribute.

The following is an example:

```cpp
#include <iostream>
using namespace std;

class Foo
```

```cpp
static int resource;
public:
    static int get_resource();
    void free_resource() { resource = 0; }
};
```

```cpp
int Foo::resource = 0; // initialize resource

int Foo::get_resource() {
    if(resource)
        return 0;
    else
        {
            resource = 1;
            return 1;
        }
}
```

```cpp
int main() {
    int ret = Foo::get_resource();
    cout << "resource = " << ret << endl;
    return 0;
}
```

```cpp
// output
resource = 1
```

Note that this example, Foo is not instantiated.

## Object Assignment

Assuming that two objects are of the same type, we can assign one object to another using the usual assignment operator =. This causes the data of the object on the right side to be bitwise copied into the object on the left.

## Local Classes

A local class is a class defined within a function. The following example defines a class within a function:

```cpp
#include <iostream>
using namespace std;

// forward declaration of function f
void f();

int main()
{
    f();
    return 0;
}
```

```cpp
void f()
{
    // define a local class inside f
class Foo {
    int i;
    public:
    void put_i(int n) { i=n; }
    int get_i() { return i; }
}

Foo foo;

```cpp
foo.put_i(10);
cout << "foo i data member = " << foo.get_i() << endl;
```

```cpp
// output
foo i data member = 10
```

There are stringent restrictions on the use of local classes:

- all member functions must be defined within the class declaration.
- The local class may not access any local variables of the function in which it is declared; except for static variables declared inside the function.
- Static variables cannot be declared inside a local class.

A local class may access typedefs and.

## C++ Namespaces

The purpose of namespaces is to localize names to avoid collisions. Prior to the invention of namespaces, if our program defined a function called abs(), could (depending upon its parameter list) override the standard library function because both names would be in the global namespace.

The creation of namespaces solves this problem. A namespace allows the same name to be used in different contexts. This is done by localizing the visibility of names to the namespace in which they are declared.

The namespace keyword allows us to partition the global namespace by creating a region. A namespace defines a scope for all the identifiers that are in it. The syntax for a namespace is:

```cpp
namespace name {
// declarations
}
```

The visibility of any name within a namespace is confined to the scope defined by it.

```cpp
namespace counter_namespace {
int upperbound;
int lowerbound;
class Counter {
int count;
public:
counter(int n) {
    if(n <= upperbound)
        count = n;
    }
}
```

```cpp
else
    count = upperbound;
}
void reset(int n)
{
    if(count > lowerbound)
        return count--;
    else
        return lowerbound;
}
```

Here the visibility of upperbound, lowerbound, and the class Counter is confined to the counter_namespace.

Identifiers declared within a namespace block can be referred to in the namespace without any namespace qualification. For example, within the namespace counter_namespace, the run() function can refer directly to lowerbound. However, since a namespace defines a scope, we need to use the scope resolution operator in order to refer to objects declared within a namespace from outside.

For example, to assign the value 10 to upperbound from code outside counter_namespace, we must use the scope resolution operator:

```cpp
counter_namespace::upperbound = 10;
```

and to declare an object of type Counter from outside counter_namespace, we use:

```cpp
counter_namespace::Counter foo;
```

## The Global Namespace

If an identifier is not declared in any namespace, it is part of the global namespace. In general, we should avoid making declarations in the global namespace, except for the entry point function main which is required to be in the global namespace.

To use an identifier such as someFunction() that is in the global namespace, we use the scope resolution operator without any prefix, as in:

```cpp
::someFunction(x);
```

## Best Practise

Whenever you want to refer to a global variable (it is in the global namespace), preface the variable with the scope resolution operator. This will let us know that the variable is defined in the global namespace. Example:

```cpp
foo(int x) {
  return x + ::y;
}
```

## Bringing An Identifier Into Scope

We can bring an identifier into the scope of another namespace by qualifying the identifier with the scope resolution operator. The syntax is as follows:

```cpp
void foo() {
  std::cout << std::string("Hello World");
}
```
