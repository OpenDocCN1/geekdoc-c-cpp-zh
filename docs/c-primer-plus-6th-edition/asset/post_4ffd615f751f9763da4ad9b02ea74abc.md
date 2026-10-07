
# Chapter 9 Memory Models and Namespaces

The third point has to do with the use and nonuse of delete. For regular new, the following statement frees up the block of memory beginning at 006E4AB0, and as a result, the next call to new is able to reuse that block:

```
delete [] pd1;
```

In contrast, the program in Listing 9.10 does not use delete to free the memory used by placement new. In fact, in this case, it can't. The memory specified by buffer is static memory, and delete can be used only with a pointer to heap memory allocated by regular new. Thus, the buffer is outside the jurisdiction of delete, and the following statement will produce a runtime error:

```
delete [] pd2; // wont work
```

On the other hand, if you use regular new to create a buffer in the first place, you can use regular delete to free that block.

Another way you can use placement new to combine it with new initialization to place information at a specific hardware address.

You may wonder exactly what the new function does. Basically, it does nothing than return the address passed to it, casting it to void * so that it can be assigned to any pointer type. That's the default placement new. C++ allows programmers to overload placement new.

The situation becomes more involved when you use placement new with class objects. Chapter 12, "Classes and Dynamic Memory Allocation," continues this story.

# Other Forms of Placement new

Just as regular new invokes a new function with one argument, the standard placement new invokes a new function with two arguments:

```
int* p1 = new int; // invokes new(sizeof(int))
int* p2 = new new(buffer) int; // invokes new(sizeof(int), buffer)
int* p3 = new(buffer) int[40]; // invokes new(40*sizeof(int), buffer)
```

The placement new is not replaceable, but it can be overloaded. It needs at least two parameters, the first of which is always a std::size_t parameter designating the number of bytes requested. Any overloaded function is termed a placement new, even if the additional parameters do not specify a location.

# Namespaces

Names in C++ can refer to variables, functions, structures, enumerations, classes, and class members. When you use class libraries projects grow large, the potential for name conflicts increases. For example, two libraries might both define class name List, Tree, and Node, but in incompatible ways. You might want the List from one library and the Tree from the other, and each might expect its own version of Node. Such conflicts are termed namespace problems.

The C++ Standard provides namespace facilities to provide greater control over the scope of names. It took a while for compilers to incorporate namespaces, but, by now, support has become common.

# Traditional C++ Namespaces

Before looking at the new namespace facilities in C++, let's review the namespace properties that already exist in C++ and introduce some terminology. This can help you make idea of namespaces seem more familiar.

One term you need to be aware of is declarative region. A declarative region is a region in which declarations can be made. For example, you can declare a global variable outside any function. The declarative region for variable is the file in which it is declared. If you declare a variable inside its function, its declarative region is the innermost block which it is declared.

A second term you need to be aware of is potential scope. The potential scope for a variable begins at its point of declaration and extends to the end of its declarative region. The potential scope is more limited than the declarative region because you't use a variable above the point where it is first defined.

However, a variable might not be everywhere in its potential scope. For instance, it might be hidden by another variable of the same name in a nested declarative region. For example, a local variable declared in a function has a global variable declared in the same file (for this variable, the declarative region is the file). The portion of the program that actually see the variable is the term scope, which is what we've been using the term all. Figures 9.5 and 9.6 illustrate the declarative region, potential scope, and scope. C++s rules about global and local variables define a kind of namespace hierarchy. Each declarative region can declare names that are independent of names declared in other declarative regions. A local variable declared in one function doesn't conflict with a local variable declared in a second function.

# New Namespace Features

C++ now adds the ability to create namespaces by defining a new kind of declarative region, whose main purpose is to provide an area in which to declare names. The names in one namespace do not conflict with the same names declared in other namespaces, and there are mechanisms for letting other parts of a program use items declared in a namespace. The following code, for example, uses the new keyword namespace to create two namespaces, Jack and Jill:

```
namespace Jack {
    double pair;
    void fetch();
    int pal;
    struct Well { ... };
}
namespace Jill {
double bucket (double n) { ... } // function definition
double fetch; // variable declaration
int pal; // variable declaration
struct Hill { ... }; // structure declaration
}
```

Namespaces can be located at the global level or inside other namespaces, but they cannot be placed in a block. Thus, a name declared in a namespace has external linkage by default (unless it refers to a constant).

In addition to user-defined namespaces, there is one more namespace, the global namespace-space. This corresponds to the file-level declaration, so what was used to be termed global variables are now described as being part of the global namespace.

The names in any one namespace do not conflict with names in another namespace. Thus, the fetch in Jack can coexist with the fetch in Jill and the Hill in Jill can coexist with an external Hill. The rules governing declarations and definitions in a namespace-space are the same as the rules for global declarations and definitions.

```cpp
#include <iostream>
using namespace std;

void orp(int);
int ro = 10;
int main() {
    int goo;
    {
        for (int i = 0; 1 < ro; i++) {
            int temp = 0;
            int goo = temp * i;
            ...
        }
        ...
        return 0;
    }
}
void orp(int ex) {
    int m;
    {
        int ro = 2;
        ...
    }
}
```

![](img/cd111a87c1db9aff4db4b18834327463_498_0.png)

Figure 9.5 Declarative regions.

# Namespaces

```cpp
#include <iostream>
using namespace std;

void orp(int);
int ro = 10;
int main() {
    int goo;
    {
        for (int i = 0; 1 < ro; i++) {
            int temp = 0;
            int goo = temp * i;
            ...
        }
        ...
        return 0;
    }
}
}
void orp(int ex) {
    int m;
    {
        int ro = 2;
        ...
    }
}
```

Figure 9.6 Potential scope and scope.

# # Memory Models and Namespaces

Of course, you need a way to access names in a given namespace. The simplest way is to use ::, the scope-resolution operator, to qualify a name with its namespace:

```
Jack::pail = 12.34;      // use a variable
Jill::Hill;                    // create a type
Jack::fetch();                      // use a function
```

An unnamed name, as such pail, is termed the unqualified name, whereas a name with the namespace, as in Jack::pail, is termed a qualified name.

# using declarations and directives

Having to qualify names every time they are used is not always an appealing prospect, so C++ provides two mechanisms—the using declaration and the using directive—to simplify using namespaces. The using declaration lets you make identifiers avoidable, and the using directive makes the entire namespace accessible.

The using declaration precedes a qualified name with the keyword using:

```
Jill::fetch;      // a using declaration
```

A using declaration adds a particular name to the declarative region in which it occurs. For example, the using declaration of Jill::fetch in main() adds fetch to the declarative region defined by main(). After making this declaration, you can use the name fetch instead of Jill::fetch. The following code fragment illustrates these points:

```cpp
namespace Jill {
double bucket(double n) { ... }
double fetch;
struct Hill { ... };
}
```

```cpp
char fetch;
int main()
{
    using Jill::fetch;      // put fetch into local namespace
    double fetch;                        // Error! Already have a local fetch
    cin >> fetch;                       // read a value into Jill::fetch
    cin >> ::fetch;                     // read a value into global namespace
}
```

Because a using declaration adds the name to the local declarative region, this example precludes creating another local variable, fetch would override a global variable by the same name.

Placing a using declaration at the external level adds the name to the global namespace:

```cpp
void other();
namespace Jack
```

```cpp
namespace Jill {
    void fetch();
}
```

```Namespaces are open, meaning that you can add names to existing namespaces. For example, the following statement adds the name goose to the existing list of names in Jill:

```cpp
namespace Jill {
    char * goose(const char *);
}
```

Similarly, the Jack namespace provides a prototype for a fetch() function. You can provide the code for the function later in the file (or another file) by using the Jack namespace:

```cpp
namespace Jack {
    void fetch()
    ...
}
```
