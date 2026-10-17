
## 7.5 Friend and Generic Functions

### 7.5.1 Friend Functions

The friend function is a non-member function of a class that has access as a normal function but is declared with the keyword friend.

### Features of Friend Functions

- Declared with the `friend` keyword only once, either with a global scope or in another class.
- It can have any type of access in a class: public, private, or protected.
- Friend functions are called upon without any object or dot operator.
- Objects can be passed as arguments.
- It has access to all data members of a class (including private), even though it is a non-member function.
- Friend relationships cannot be inherited.

The syntax for a friend function is as follows:

```cpp
class OurClass
{
    //body
    friend returnType Myfunction(Parameters list...);
};
```

### Code: Using the Friend Function

```cpp
#include <iostream>
using namespace std;
class myclass
{
    friend int myfriend(int a, int b);
};
int myfriend(int a, int b)
{
    return a+b;
}
int main()
{
    int a,b;
    cout<<"Enter numbers to add"<<endl;
    cin>>a>>b;
    cout<<"Addition gives "<<myfriend(a,b)<<endl;
    return 0;
}
```

**Output:**

```text
Enter numbers to add
23
567
Addition gives 590
```

**Code Debriefing:**

- This code shows how the friend function is made.
- This function can be declared inside a class and defined outside the class.

### 7.5.2 Generic Functions

In a situation where a normal function is used more than once, we need parameters on which the function acts to be of different data types. This is made possible using generic functions in C++. These act as a template for different types of parameters to give the desired results.

### Features of Generic Functions

- Act like macros and body expanded at compile time to receive arguments.
- Source code serves as a template and so the code is the same for all functions, but when the different copies of the code are compiled, there are differing results because there are different argument types.
- Class templates can also be used in a similar fashion as generic functions.
- These functions help decrease function overloading.
- Parameters can also be given a default value, if needed.

The syntax for a generic function is as follows:

```cpp
template <typename T> T mytemplate(T parameter1, T parameter2)
{
    //template body
}
```

### Code: Generic Functions and Swapping Numbers

```cpp
#include <iostream>
using namespace std;
class myclass
{
    public:
    void swapR(int &a,int &b)
    {
        cout<<"Swapping using the call by reference changes what is visible "<<endl;
        a= a+b;
        b= a-b;
        a= a-b;
    }
    void swapP(int *a,int *b)
    {
        cout<<"Swapping by using the call by pointers "<<endl;
        *a= *a + *b;
        *b= *a - *b;
        *a= *a - *b;
    }
}c1;
int main()
{
    int a,b;
    cout<<"Enter numbers to swap"<<endl;
    cin>>a>>b;
    cout<<"After swapping A= "<<a<<" B="<<b<<endl;
    c1.swapR(a,b);
    cout<<"After swapping A= "<<a<<" B="<<b<<endl;
    c1.swapP(&a,&b);
    cout<<"After swapping A= "<<a<<" B="<<b<<endl;

    return 0;
}
```

**Output:**

```text
Enter numbers to swap
23
67
After swapping A= 23 B=67
Swapping using the call by reference changes what is visible
After swapping A= 67 B=23
Swapping by using the call by pointers
```

### Code: Using a Template to Swap Numbers

```cpp
#include<iostream>
using namespace std;

template <class T, class T1>
void swap(T &a,T1 &b)
{
        T temp=a;
        a=b;
        b=temp;
}

int main()
{
```

The syntax for a namespace is as follows:

```cpp
namespace Ournamespace
{
    // namespace body
}
Ournamespace :: identifiers_any;
```

### Code: Using Namespace

```cpp
#include <iostream>
using namespace std;

namespace ourSpace1
{
void nFunc()
{
    cout << "\nFunction of ourSpace1 called" << endl;
}
}

namespace ourSpace2
{
void nFunc()
{
    cout << "\nFunction of ourSpace2 called" << endl;
}
}

int main ()
{
    ourSpace1::nFunc();
    ourSpace2::nFunc();
    return 0;
}
```

**Output:**

```text
Function of ourSpace1 called
Function of ourSpace2 called
```

**Code Debriefing:**

- In this code, the namespaces are declared.
- Two functions are defined inside the namespaces.
- The function `nFunc` is called upon using the scope resolution operator.

## Summary

- Polymorphism allows for multiple forms of a method with different signatures but the same name.
- Methods made can exist in multiple forms by varying in type of parameters and number of parameters they take in the signature of a function.
- Dynamic or late binding tells which procedure will be called at runtime.
- Static or early binding tells which procedure will be called at compile time.
- C++ provides interfaces that lead to no direct implementation and only declare methods.
- A *virtual function* is a type of function that is declared as well as defined in the parent or base class and redefined in the child class.
- A *pure virtual function* is a type of function that is only declared but never implemented or redefined.
- The abstract class (ABC) is a type of class that has only pure virtual functions. This means that it is only declared and never defined; this helps all child classes to inherit and redefine the members as they wish, too.
- Function overloading is done by giving functions the same name but different signatures.
- Function overriding is done by giving functions the same name and signatures.
- A *friend* function is a non-member function of a class that has access as a normal function but is declared with the keyword `friend`.
- Generic functions in C++ act as a template and use different types of parameters to give the desired results.
- *Namespaces* logically organize identifiers (variables, methods, and classes) so they can be defined and declared under one name or a space.

## Exercises

### Theory Questions

1. What is polymorphism in C++? Describe the syntax for using it with examples.
2. What are the different types of polymorphism available in C++?
3. What is the difference between compile time and runtime polymorphism?
4. Discuss the concept of virtual and pure virtual functions in C++?
5. What is meant by dynamic and static binding?
6. How is runtime polymorphism implemented in C++? Explain with examples.
7. What are abstract classes? Explain few of their features.
8. What is the use of a friend function in C++? Explain a few of its features.
9. What are templates in C++? Explain few of its features and how they are declared.
10. What are namespaces in C++? Explain few of their features.
11. Draw parallels between abstract and virtual functions in C++.

### Practical Questions

1. Write a program in C++ to demonstrate the use of runtime polymorphism.
2. Write a program in C++ illustrating the use of pure virtual functions.
3. Write a program in C++ to depict the use of the abstract keyword.
4. Write a program in C++ to maintain an ecommerce database using virtual functions.
5. Write a program in C++ to use the concept of templates to find the average of five inputs.
6. Write a program in C++ to depict the use of an abstract base class.
7. Write a program in C++ to implement the concept of namespaces.
8. Write a program in C++ to show a student database using various aspects of polymorphism.
