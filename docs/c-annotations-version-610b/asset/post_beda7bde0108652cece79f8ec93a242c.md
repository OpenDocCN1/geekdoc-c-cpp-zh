
amplifier() const member function and leave it to the application to set up its own interface to the amplifier. Alternatively, a revised class could define members for setting the volume of either the NavSet or the ComSet parts.

In situations where two base classes offer identically named members special provisions need to be made to prevent ambiguity:

- The intended base class can explicitly be specified using the base class name and scope resolution operator:

```cpp
NavComSet navcom(intercom, dial);

navcom.NavSet::setVolume(5);    // sets the NavSet volume level
navcom.ComSet::setVolume(5);    // sets the ComSet volume level
```

- The class interface is provided with member functions that can be called unambiguously. These additional members are usually defined inline:

```cpp
class NavComSet: public ComSet, public NavSet
{
    public:
        NavComSet(Intercom &intercom, VHF_Dial &dial);
        void comVolume(size_t volume);
        void navVolume(size_t volume);
};
inline void NavComSet::comVolume(size_t volume)
{
    ComSet::setVolume(volume);
}
inline void NavComSet::navVolume(size_t volume)
{
    NavSet::setVolume(volume);
}
```

- If the NavComSet class is obtained from a third party, and cannot be modified, a disambiguating wrapper class may be used:

```cpp
class MyNavComSet: public NavComSet
{
    public:
        MyNavComSet(Intercom &intercom, VHF_Dial &dial);
        void comVolume(size_t volume);
        void navVolume(size_t volume);
};
inline MyNavComSet::MyNavComSet(Intercom &intercom, VHF_Dial &dial)
:
    NavComSet(intercom, dial);
{}
inline void MyNavComSet::comVolume(size_t volume)
{
    ComSet::setVolume(volume);
}
inline void MyNavComSet::navVolume(size_t volume)
{
    NavSet::setVolume(volume);
}
```

## 13.8 Conversions between base classes and derived classes

When public inheritance is used to define classes, an object of a derived class *is* at the same time an object of the base class. This has important consequences for object assignment and for the situation where pointers or references to such objects are used. Both situations are now discussed.

### 13.8.1 Conversions with object assignments

Continuing our discussion of the `NavCom` class, introduced in section 13.7, we now define two objects, a base class and a derived class object:

```cpp
ComSet com(intercom);
NavComSet navcom(intercom2, dial2);
```

The object `navcom` is constructed using an `Intercom` and a `VHF_Dial` object. However, a `NavComSet` is at the same time a `ComSet`, allowing the assignment *from* `navcom` (a derived class object) *to* `com` (a base class object):

```cpp
com = navcom;
```

The effect of this assignment is that the object `com` now communicates with `intercom2`. As a `ComSet` does not have a `VHF_Dial`, the `navcom`'s `dial` is ignored by the assignment. When assigning a base class object from a derived class object only the base class data members are assigned, other data members are dropped, a phenomenon called *slicing*. In situations like these slicing probably does not have serious consequences, but when passing derived class objects to functions defining base class parameters or when returning derived class objects from functions returning base class objects slicing also occurs and might have unwelcome side-effects.

The assignment from a base class object to a derived class object is problematic. In a statement like

```cpp
navcom = com;
```

it isn't clear how to reassign the `NavComSet`'s `VHF_Dial` data member as they are missing in the `ComSet` object `com`. Such an assignment is therefore refused by the compiler. Although derived class objects are also base class objects, the reverse does not hold true: a base class object is not also a derived class object.

The following general rule applies: in assignments in which base class objects and derived class objects are involved, assignments in which data are dropped are legal (called *slicing*). Assignments in which data remain unspecified are *not* allowed. Of course, it is possible to overload an assignment operator to allow the assignment of a derived class object from a base class object. To compile the statement

```cpp
navcom = com;
```

the class `NavComSet` must have defined an overloaded assignment operator accepting a `ComSet` object for its argument. In that case it's up to the programmer to decide what the assignment operator will do with the missing data.

### 13.8.2 Conversions with pointer assignments

We return to our `Vehicle` classes, and define the following objects and pointer variable:

```cpp
Land land(1200, 130);
```

The initialization of a dynamically allocated object usually consists of a two-step process: first the array is allocated (implicitly calling the default constructor); second the array’s elements are initialized, as in the following little example:

```cpp
string *sp = new string[10];
fill(sp, sp + 10, string("hello world"));
```

These approaches all suffer from ‘double initializations’, comparable to not using member initializers in constructors.

One way to avoid double initialization is to use inheritance. Inheritance can profitably be used to call non-default constructors in combination with operator new[]. The approach capitalizes on the following:

- A base class pointer may point to a derived class object;
- A derived class without (non-static) data members has the same size as its base class.

The above also suggests a possible approach:

- Derive a simple, member-less class from the class we’re interested in;
- Use the appropriate base class initializer in its default constructor;
- Allocate the required number of derived class objects, and assign new[]’s return expression to a pointer to base class objects.

Here is a simple example, producing 10 lines containing the text hello world:

```cpp
#include <iostream>
#include <string>
#include <algorithm>
#include <iterator>

using namespace std;

struct Xstr: public string
{
    Xstr()
    :
        string("hello world")
    {}
};

int main()
{
    string *sp = new Xstr[10];
    copy(sp, sp + 10, ostream_iterator<string>(cout, "\n"));
}
```

Of course, the above example is fairly unsophisticated, but it’s easy to polish the example: the class Xstr can be defined in an anonymous namespace, accessible only to a function getString() which may be given a size_t nObjects parameter, allowing users to specify the number of hello world-initialized strings they would like to allocate.

Instead of hard-coding the base class arguments it’s also possible to use variables or functions providing the appropriate values for the base class constructor’s arguments. In the next example a local class Xstr is defined inside a function nStrings(size_t nObjects, char const *fname), expecting

A completely different way to avoid the double initialization (not using inheritance) is to use placement new (cf. section 9.1.5): simply allocate the required amount of memory followed by the proper in-place allocation of the objects, using the appropriate constructors. The following example can also be used in multithreaded environments. The approach uses a pair of static construct/destroy members to perform the required initialization.

In the program shown below construct expects an istream that provides the initialization strings for objects of a class String simply containing a std::string object. Construct first allocates enough memory for the n String objects plus room for an initial size_t value. This initial size_t value is then initialized with n. Next, in a for statement, lines are read from the provided stream and the lines are passed to the constructors, using placement new calls. Finally the address of the first String object is returned.

The member destroy handles the destruction of the objects. It retrieves the number of objects to destroy from the size_t it finds just before the location of the address of the first object to destroy. The objects are then destroyed by explicitly calling their destructors. Finally the raw memory, originally allocated by construct is returned.

```cpp
#include <fstream>
#include <iostream>
#include <string>
using namespace std;

class String
{
    union Ptrs
    {
        void *vp;
        String *sp;
        size_t *np;
    };

    std::string d_str;

    public:
        String(std::string const &txt)
        :
            d_str(txt)
        {}
        ~String()
        {
            cout << "destructor: " << d_str << '\n';
        }
        static String *construct(istream &in, size_t n)
        {
            Ptrs p = {operator new(n * sizeof(String) + sizeof(size_t))};
            *p.np++ = n;

            string line;
            for (size_t idx = 0; idx != n; ++idx)
            {
                getline(in, line);
                new(p.sp + idx) String(line);
            }

            return p.sp;
        }
        static void destroy(String *sp)
        {
```
