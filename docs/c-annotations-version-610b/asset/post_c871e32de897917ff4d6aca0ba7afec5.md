
```cpp
{
    public:
        std::string const &name()    const;
        std::string const &address()  const;
        std::string const &phone()    const;
        size_t mass()                 const;
};
```

The rule of thumb given in section 3.1.3 applies here too: whichever appears to the left of the keyword `const` is not altered. With member functions this should be interpreted as ‘doesn’t alter its own data’.

When implementing a const member function, the const attribute must be repeated:

```cpp
string const &Person::name() const
{
    return d_name;
}
```

The compiler prevents the data members of a class from being modified by one of its const member functions. Therefore, a statement like

```cpp
d_name[0] = toupper(static_cast<unsigned char>(d_name[0]));
```

results in a compiler error when added to the above function’s definition.

Const member functions are used to prevent inadvertent data modification. Except for constructors and the destructor (cf. chapter 9), only const member functions can be used with (plain, references or pointers to) const objects.

Const objects are frequently encountered as `const &` parameters of functions. Inside such functions, only the object’s const members may be used. Here is an example:

```cpp
void displayMass(ostream &out, Person const &person)
{
    out << person.name() << " weighs " << person.mass() << " kg.\n";
}
```

Since person is defined as a Person const &, the function displayMass cannot call, e.g., `person.setMass(75)`.

The const member function attribute can be used to overload member functions. When functions are overloaded by their const attribute, the compiler uses the member function matching most closely the const-qualification of the object:

- When the object is a `const` object, only const member functions can be used.
- When the object is not a `const` object, non-const member functions are used, unless only a const member function is available. In that case, the const member function is used.

The next example illustrates how (non) const member functions are selected:

```cpp
#include <iostream>
using namespace std;

class Members
{
    public:
        Members();
        void member();
        void member() const;
};
```

```cpp
Members::Members()
{}
void Members::member()
{
    cout << "non const member\n";
}
void Members::member() const
{
    cout << "const member\n";
}
```

```cpp
int main()
{
    Members const constObject;
    Members       nonConstObject;

    constObject.member();
    nonConstObject.member();
}
/*
        Generated output:

    const member
    non const member

*/
```

As a general principle of design: member functions should always be given the `const` attribute, unless they actually modify the object’s data.

### 7.6.1 Anonymous objects

Sometimes objects are used because they offer a certain functionality. The objects only exist because of their functionality, and nothing in the objects themselves is ever changed. The following class `Print` offers a facility to print a string, using a configurable prefix and suffix. A partial class interface could be:

```cpp
class Print
{
    public:
        Print(ostream &out);
        void print(std::string const &prefix, std::string const &text,
                   std::string const &suffix) const;
};
```

An interface like this would allow us to do things like:

```cpp
Print print(cout);
for (int idx = 0; idx != argc; ++idx)
    print.print("arg: ", argv[idx], "\n");
```

This works fine, but it could greatly be improved if we could pass `print`’s invariant arguments to `Print`’s constructor. This would simplify `print`’s prototype (only one argument would need to be passed rather than three) and we could wrap the above code in a function expecting a `Print` object:

```cpp
void allArgs(Print const &print, int argc, char *argv[])
{
    for (int idx = 0; idx != argc; ++idx)
        print.print(argv[idx]);
}
```

The above is a fairly generic piece of code, at least it is with respect to `Print`. Since `prefix` and `suffix` don't change, they can be passed to the constructor which could be given the prototype:

```cpp
Print(ostream &out, string const &prefix = "", string const &suffix = "");
```

Now `allArgs` may be used as follows:

```cpp
Print p1(cout, "arg: ", "\n");        // prints to cout
Print p2(cerr, "err: --", "--\n");    // prints to cerr

allArgs(p1, argc, argv);              // prints to cout
allArgs(p2, argc, argv);              // prints to cerr
```

But now we note that `p1` and `p2` are only used inside the `allArgs` function. Furthermore, as we can see from `print`'s prototype, `print` doesn't modify the internal data of the `Print` object it is using.

In such situations it is actually not necessary to define objects before they are used. Instead *anonymous objects* may be used. Anonymous objects can be used:

- to initialize a function parameter which is a `const` reference to an object;
- if the object is *only* used inside the function call.

These anonymous objects are considered constant as they merely exist for passing the information of (class type) objects to functions. They are not considered 'variables'. Of course, a `const_cast` could be used to cast away the const reference's constness, but any change is lost once the function returns. These anonymous objects used to initialize const references should not be confused with rvalue references (section 3.3.2), which have a completely different purpose in life. Rvalue references primarily exist to be 'swallowed' by functions receiving them. Thus, the information made available by rvalue references outlives the rvalue reference objects which are also anonymous.

Anonymous objects are defined when a constructor is used without providing a name for the constructed object. Here is the corresponding example:

```cpp
allArgs(Print(cout, "arg: ", "\n"), argc, argv);   // prints to cout
allArgs(Print(cerr, "err: --", "--\n"), argc, argv); // prints to cerr
```

In this situation the `Print` objects are constructed and immediately passed as first arguments to the `allArgs` function, where they are accessible as the function's `print` parameter. While the `allArgs` function is executing, they can be used, but once the function has completed, the anonymous `Print` objects are no longer accessible.

### 7.6.2 Subtleties with anonymous objects

Anonymous objects can be used to initialize function parameters that are `const` references to objects. These objects are created just before such a function is called, and are destroyed once the function has terminated. C++'s grammar allows us to use anonymous objects in other situations as well. Consider the following snippet of code:

```cpp
int main()
{
    // initial statements
    Print("hello", "world");
    // later statements
}
```

In this example an anonymous Print object is constructed, and it is immediately destroyed thereafter. So, following the 'initial statements' our Print object is constructed. Then it is destroyed again followed by the execution of the 'later statements'.

The example illustrates that the standard lifetime rules do not apply to anonymous objects. Their lifetimes are limited to the *statements*, rather than to the *end of the block* in which they are defined.

Plain anonymous objects are at least useful in one situation. Assume we want to put *markers* in our code producing some output when the program's execution reaches a certain point. An object's constructor could be implemented so as to provide that marker-functionality, allowing us to put markers in our code by defining anonymous, rather than named objects.

C++'s grammar contains another remarkable characteristic illustrated by the next example:

```cpp
int main(int argc, char **argv)
{
    Print p(cout, "", "");        // 1
    allArgs(Print(p), argc, argv); // 2
}
```

In this example a non-anonymous object p is constructed in statement 1, which is then used in statement 2 to initialize an anonymous object. The anonymous object, in turn, is then used to initialize allArgs's const reference parameter. This use of an existing object to initialize another object is common practice, and is based on the existence of a so-called *copy constructor*. A copy constructor creates an object (as it is a constructor) using an existing object's characteristics to initialize the data of the object that's created. Copy constructors are discussed in depth in chapter 9, but presently only the concept of a copy constructor is used.

In the above example, a copy constructor is used to initialize an anonymous object. The anonymous object was then used to initialize a parameter of a function. However, when we try to apply the same trick (i.e., using an existing object to initialize an anonymous object) to a plain statement, the compiler generates an error: the object p can't be redefined (in statement 3, below):

```cpp
int main(int argc, char *argv[])
{
    Print p("", "");              // 1
    allArgs(Print(p), argc, argv); // 2
    Print(p);                     // 3 error!
}
```

Does this mean that using an existing object to initialize an anonymous object that is used as a function argument is OK, while an existing object can't be used to initialize an anonymous object in a plain statement?

The compiler actually provides us with the answer to this apparent contradiction. About statement 3, the compiler reports something like:

```text
error: redeclaration of 'Print p'
```
