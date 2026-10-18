
- A constructor may be declared **explicit** to make the conversion explicit.
- We can make a data item of a **const** object or function modifiable by declaring it **mutable**.
- ANSI C++ permits us to define our own **namespace** scope in our program to overcome certain name conflict situations.
- Namespaces may be nested.
- Members of **namespace** scope may be accessed using either **using** declaration or **using** directive.
- ANSI C++ proposes keywords that may be used in place of symbols for certain operators.
- In new standard, the header files should be specified without .h extension and the **using** directive `using namespace std;` should be added in every program.
- Some old style header files are renamed in the new standard. For example, **math.h** file is known as **cmath**.

## Key Terms

**and** | **and_eq** | ANSI C++ | **bitand** | **bitor** | **bool** | Boolean | C-type casting | C++ standard | C++ type casting | casts | **compl** | **const** | **const** function | **const** object | **const_cast** | constant casts | current scope | downcast | **dynamic_cast** | dynamic casts | **explicit** constructor | false value | global identifiers | **header** file | implicit conversion | **mutable** member | name() function | **namespace** scope | nesting namespaces | not | not_eq | operator keywords | or | or_eq | polymorphic objects | reinterpret casts | reinterpret_cast | RTTI | source type | standard library | static casts | **static_cast** | std namespace | target type | **true value** | type casts | **type_info** class | type-safe casting | **typeid** | **typeinfo** header | unnamed namespaces | **using** declaration | **using** directive | **using namespace** | **volatile** | **wchar_t** | wide-character literal | **xor** | **xor_eq**

## Review Questions

- 16.1 List the two data types added by the ANSI C++ standard committee.
- 16.2 What is the application of **bool** type variables?
- 16.3 What is the need for **wchar_t** character type?
- 16.4 List the new operators added by the ANSI C++ standard committee.
- 16.5 What is the application of **const_cast** operator?
- 16.6 Why do we need the operator **static_cast** while the old style cast does the same job?
- 16.7 How does the **reinterpret_cast** differ from the **static_cast**?
- 16.8 What is dynamic casting? How is it achieved in C++?
- 16.9 What is **typeid** operator? When is it used?
- 16.10 What is explicit conversion? How is it achieved?
- 16.11 When do we use the keyword **mutable**?
- 16.12 What is a namespace conflict? How is it handled in C++?
- 16.13 How do we access the variables declared in a named namespace?
- 16.14 What is the difference between using the **using namespace** directive and using the **using** declaration for accessing **namespace** members?
- 16.15 What is wrong with the following code segment?

```cpp
const int m = 100;
int *ptr = &m;
```

- 16.16 What is the problem with the following statements?

```cpp
const int m = 100;
double *ptr = const_cast<double*>(&m);
```

- 16.17 What will be the output of the following program?

```cpp
#include<iostream.h>
class Person
{
        // ....
};
int main()
{
        Person John;
        cout << " John is a ";
        cout << typeid(John).name() << "\n";
}
```

- 16.18 What is wrong with the following namespace definition?

```cpp
namespace Main
{
        int main()
        {
                // ....
        }
}
```

## Debugging Exercises

- **16.1** Identify the error in the following program.

```cpp
#include <iostream>
class A
{
public:
        A()
        {
        }
        A(int i)
        {
        }
};
class B
{
public:
        B()
        {
        }
        explicit B(int)
        {
        }
};
void main()
{
        A a1=12;
        A a2;
        A a3=a1;
        B b1 = 12;
}
```

- **16.2** Identify the error in the following program.

```cpp
#include <iostream.h>

class A
{
protected:
    int i;

public:
    A()
    {
        i = 10;
    }
    int get()
    {
        return i;
    }
};

class B: public A
{
public:
    B()
    {
    }
    int get()
    {
        return i + i;
    }
};

void main()
{
    A *a = new A();
    B *b = static_cast<B*>(a);
    cout << b->get();
}
```

- **16.3** Identify the error in the following program.

```cpp
#include <iostream.h>

namespace A
{
    int i;
    void displ()
    { 
        cout << i; 
    }
}
void main()
{
    namespace Inside
    { 
        int inside1;
        void displnInside()
        { 
            cout << inside1; 
        }
    }
}
A::i = 10;
cout << A::i;
A::displ();
Inside::inside1 = 20;
cout << Inside::inside1;
Inside::displnInside();
}
```

## Programming Exercises

- 16.1 Write a program to demonstrate the use of reinterpret_cast operator WEB.
- 16.2 Define a namespace named Constants that contains declarations of some constants. Write a program that uses the constants defined in the namespace Constants WEB.

## Object-Oriented Systems Development

## Key Concepts

Software development components | Procedure-oriented development tools | Object-oriented paradigm | OOP notations and graphs | Data flow diagrams | Object-oriented design | Top-down decomposition | System implementation | Procedure-oriented paradigm | Classic software development life cycle | Fountain model | Object-oriented analysis | Textual analysis | Class hierarchies | Structured design | Prototyping paradigm

Software engineers have been trying various *tools, methods,* and *procedures* to control the process of software development in order to build high-quality software with improved productivity. The methods provide “how-to’s” for building the software while the tools provide automated or semi-automated support for the methods. They are used in all the stages of software development process, namely, planning, analysis, design, development and maintenance. The software development procedures integrate the methods and tools together and enable rational and timely development of software systems (Fig. 17.1). They provide guidelines as to how to apply the methods and tools, how to produce the deliverables at each stage, what controls to apply, and what milestones to use to assess the progress.

![](img/62b7c32e48e4f960a8dc2825a7119fb2_681_0.png)

**Fig. 17.1** Software development components

There exist a number of software development paradigms, each using a different set of methods and tools. The selection of a particular paradigm depends on the nature of the application, the programming language used, and the controls and deliverables required. The development of a successful system depends not only on the use of the appropriate methods and techniques but also on the developer’s commitment to the objectives of the system. A successful system must:

- 1. satisfy the user requirements,
- 2. be easy to understand by the users and operators,
- 3. be easy to operate,
- 4. have a good user interface,
- 5. be easy to modify,
- 6. be expandable,
- 7. have adequate security controls against misuse of data,
- 8. handle the errors and exceptions satisfactorily, and
- 9. be delivered on schedule within the budget.

This phase translates the requirements into a representation of the software. This stage answers the questions of *how*.

*Coding:* Coding refers to the translation of the design into machine-readable form. The more detailed the design, the easier is the coding, and better its reliability.

![](img/62b7c32e48e4f960a8dc2825a7119fb2_683_0.png)

**Fig. 17.2** *Classic software development life cycle (Embedded ‘water-fall’ mode)*

*Testing:* Once the code is written, it should be tested rigorously for correctness of the code and results. Testing may involve the
