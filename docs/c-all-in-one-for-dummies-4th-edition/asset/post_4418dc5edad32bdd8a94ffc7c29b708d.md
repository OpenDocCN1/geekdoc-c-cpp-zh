
```cpp
class Prince : public King {
public:
    string School;
};

void KingInfo(King *inst) {
    cout << "=========" << endl;
    cout << inst->MyName() << endl;
    Prince *asPrince = dynamic_cast<Prince *>(inst);
    if (asPrince != 0)
    {
        cout << asPrince->School << endl;
    }
}

int main() {
    Prince George;
    George.MyName() = "George I";
    George.School = "School of the Kings";
    KingInfo(&George);
    King Henry;
    Henry.MyName() = "Henry II";
    KingInfo(&Henry);
    return 0;
}
```

When you run this code, you see output that looks like this:

```
=========
George I
School of the Kings
=========
Henry II
```

Some strange things are going on in this code. Starting with `main()`, the code calls `KingInfo()`, first passing it the address of George (a Prince instance, derived from King) and then the address of Henry (a King instance).

The `KingInfo()` function first prints the information that is common to both due to inheritance using the `MyName()` function and prints the resulting name. Then comes the important part: the dynamic cast. To do the dynamic cast, the code calls `dynamic_cast` and saves `inst` (which can be of type `King` or `Prince`) in a pointer variable called `asPrince`. Notice the syntax of `dynamic_cast`. It looks like a template in that you include a type in angle brackets. Then you put the variable you want to cast in parentheses (in this case inst).

If the dynamic cast works, it returns a pointer that you can save as the type inside angle brackets. Otherwise, the dynamic cast returns 0. After calling dynamic_cast, the code tests the result against 0. If the result is not 0, the dynamic cast worked, which means that inst is of type Prince. Then, in the if block, the code retrieves and prints the School member, which is part of Prince, not King.

Notice the unique design of the King class in Listing 2–2. For dynamic_cast to work, the base class involved must have at least one virtual function. Thus the base class — and each of its derived classes — has a virtual table (also needed for dynamic_cast to work). In addition, the Code::Blocks compiler raises a warning message when you don’t provide a virtual destructor:

```
warning: 'class King' has virtual functions but non-virtual
destructor
```

Consequently, the example includes a virtual destructor as well. Notice also that this class uses good design by keeping CrownName private and providing an accessor function, MyName(), to it.

![](img/128ab511de4e7360e167e3b15cdd5dd0_545_0.png)

You don’t need to use references in a class as shown here to make dynamic_cast work. But you do need at least one virtual function.

The fundamental difference between an old-style direct cast and a dynamic_cast is that the compiler generates code that automatically does an old-style cast, regardless of whether the cast is valid, during compile time. That is, the cast is hardcoded. But dynamic_cast tests the types at runtime. The dynamic cast may or may not work depending on the type of the object.

When you use a dynamic cast, you can cast either a pointer or a reference. The KingInfo() function shown previously in Listing 2–2 uses a pointer. Here’s a modified form that uses a reference:

```
void KingInfoAsReference(King &inst) {
    cout << "===========" << endl;
    cout << inst.MyName() << endl;
    try {
        Prince &asPrince = dynamic_cast<Prince &>(inst);
        cout << asPrince.School << endl;
    } catch (...) { }
}
```

To make this version work, you have to use an exception handler (which is a way to deal with unusual situations; see Chapter 3 in this minibook for more information on exception handlers). The reason for using an exception handler is that with a pointer, you can simply test the result against 0. But with references, you have no such thing as a null reference or 0 reference. The reference must work or you get a runtime error. In C++, the way you can catch a situation that didn’t work is by typing the word try, followed by your code that attempts to do the job, in braces. Follow that with the word catch and a set of parentheses containing three periods. Following that, you put braces — and possibly any code you want to run — just in case the earlier code didn’t work.

This code doesn’t do anything inside the catch block because the application will continue to work even if the call fails — the output simply lacks the school name. C++ requires that all try blocks are matched with a catch block, so you must include the catch block even when it doesn’t do anything.

### Statically casting with static_cast

The ANSI C++ standard includes a special type of cast that does no type checking. If you have to cast directly without the help of dynamic_cast, you should opt for static_cast instead of the old C-style cast.

When you want to do a static cast, call static_cast and follow it with angle brackets containing the type you want to cast to. Then put the item being cast inside parentheses, as in the following:

```
FinalType *f = static_cast<FinalType *>(orig);
```

The advantage of using static_cast is that it does some type checking at compile time, whereas old C-style casts do not. The compiler allows you to do static_cast only between related objects. You can do a static_cast from an instance of one class to an instance of a derived or base class. But if two classes are not related, you will get a compiler error. For example, suppose that you have these two lines of code:

```
class FinalType {};
class AnotherType {};
```

They’re unrelated classes. Then, if you have these lines of code

```
AnotherType *orig = new AnotherType;
FinalType *f = static_cast<FinalType *>(orig);
```

```cpp
#include <iostream>

using namespace std;

void PrintIt(int *out) {
    cout << "The value is: " << *out << endl;
}

int main() {
    volatile int X = 20;
    const int Y = 30;

    PrintIt(const_cast<int*>(&X));
    PrintIt(const_cast<int*>(&Y));
    return 0;
}
```

In the first case, if you were to try PrintIt(&X), you'd see error: invalid conversion from 'volatile int*' to 'int*' during compilation. Likewise, in the second case, PrintIt(&Y) would produce an error: invalid conversion from 'const int*' to 'int*' error message. Of course, neither X nor Y has its attributes removed; you simply strip the volatile or const attribute off for the purpose of sending the value to PrintIt().

## Structuring Your Data

Before C++ came to life, C had something that was similar to classes, called structures. The difference was that structures had only properties — no methods. Here's an example of a structure:

```cpp
struct Dimensions {
    int height;
    int width;
    int depth;
    int weight;
    int price;
};
```

This block of code is similar to a class; as you can see, it has some properties but no methods. Nor does it have any access control (such as public, private, or protected).

But not only did the designers of C++ add classes to C++, they also enhanced the structures in C++. So now you can use structures more powerfully in C++ than you could in C. The main change to structures in C++ is that they can have methods and access control. Thus, you can add to the `Dimensions` structure like so (making `struct` and `class` equivalent):

```cpp
struct Dimensions {
private:
    int price;
public:
    int height;
    int width;
    int depth;
    int weight;
    int GetPrice() { return price; }
};
```

Then create an instance of `Dimensions` in your code like this:

```cpp
Dimensions FirstItem;
Dimensions *SecondItem = new Dimensions;
```

> **REMEMBER**
> 
> When the great founder of the C++ language (Bjarne Stroustrup) created C++, he enhanced structures to the point that classes and structures are *identical*, with one exception. Members of a structure are public by default. Members of a class, however, are private by default. Because the differences are so small, most C++ programmers today never even touch a structure, except to create an object that has only public properties.

In other words, programmers use `struct` for simple data types that are a collection of smaller data types. (That is, they use `struct`s the same way C originally used them.) The sections that follow tell you about some of these data-structure issues.

> **TECHNICAL STUFF**
> 
> If you're familiar with C and just learning C++, you may be interested to know that when you declare a variable that is a structure type, in C++ you need to give only the name of the structure. You no longer need the word `struct` in the declaration. Thus the following line will still compile in C++:

```cpp
struct Dimensions another;
```

but all you really need is

```cpp
Dimensions another;
```
