
In fact, the compiler won’t let you use both of these using declarations because of the ambiguity that would be created.

## using Directives Versus using Declarations

Using a using directive to import all the names from a namespace wholesale is not the same as using multiple using declarations. It’s more like the mass application of a scope-resolution operator. When you use a using declaration, it is as if the name is declared at the location of the using declaration. If a particular name is already declared in a function, you can’t import the same name with a using declaration. When you use a using directive, however, name resolution takes place as if you declared the names in the smallest declarative region containing both the using directive and the namespace itself. For the following example, that would be the global namespace. If you use a using directive to import a name that is already declared in a function, the local name will hide the namespace name, just as it would hide a global variable of the same name. However, you can still use the scope-resolution operator, as in the following example:

```cpp
namespace Jill {
    double bucket(double n) { ... }
    double fetch;
    struct Hill { ... };
}
char fetch;                 // global namespace
int main()
{
    using namespace Jill;       // import all namespace names
    Hill Thrill;                // create a type Jill::Hill structure
    double water = bucket(2);   // use Jill::bucket();
    double fetch;               // not an error; hides Jill::fetch
    cin >> fetch;               // read a value into the local fetch
    cin >> ::fetch;             // read a value into global fetch
    cin >> Jill::fetch;         // read a value into Jill::fetch
    ...
}

int foom()
{
    Hill top;                   // ERROR
    Jill::Hill crest;            // valid
}
```

Here, in main(), the name Jill::fetch is placed in the local namespace. It doesn’t have local scope, so it doesn’t override the global fetch. But the locally declared fetch hides both Jill::fetch and the global fetch. However, both of the last two fetch variables are available if you use the scope-resolution operator. You might want to compare this example to the preceding one, which uses a using declaration.

Instead, you should use this:

```cpp
int x;
std::cin >> x;
std::cout << x << std::endl;
```

Or you could use this:

```cpp
using std::cin;
using std::cout;
using std::endl;
int x;
cin >> x;
cout << x << endl;
```

You can use nested namespaces, as described in the following section, to create a namespace that holds the using declarations you commonly use.

## More Namespace Features

You can nest namespace declarations, like this:

```cpp
namespace elements
{
    namespace fire
    {
        int flame;
        ...
    }
    float water;
}
```

In this case, you refer to the `flame` variable as `elements::fire::flame`. Similarly, you can make the inner names available with this using directive:

```cpp
using namespace elements::fire;
```

Also you can use using directives and using declarations inside namespaces, like this:

```cpp
namespace myth
{
    using Jill::fetch;
    using namespace elements;
    using std::cout;
    using std::cin;
}
```

Suppose you want to access `Jill::fetch`. Because `Jill::fetch` is now part of the `myth` namespace, where it can be called `fetch`, you can access it this way:

```cpp
std::cin >> myth::fetch;
```

Of course, because it is also part of the Jill namespace, you still can call it

```cpp
Jill::fetch;
std::cout << Jill::fetch;  // display value read into myth::fetch
```

Or you can do this, provided that no local variables conflict:

```cpp
using namespace myth;
cin >> fetch;           // really std::cin and Jill::fetch
```

Now consider applying a using directive to the myth namespace. The using directive is transitive. We say that an operation op is transitive if A op B and B op C implies A op C. For example, the > operator is transitive. (That is, A bigger than B and B bigger than C implies A bigger than C.) In this context, the upshot is that the following statement places both the myth and the elements namespaces in scope:

```cpp
using namespace myth;
```

This single directive has the same effect as the following two directives:

```cpp
using namespace myth;
using namespace elements;
```

You can create an alias for a namespace. For example, suppose you have a namespace defined as follows:

```cpp
namespace my_very_favorite_things { ... };
```

You can make mvft an alias for my_very_favorite_things by using the following statement:

```cpp
namespace mvft = my_very_favorite_things;
```

You can use this technique to simplify using nested namespaces:

```cpp
namespace MEF = myth::elements::fire;
using MEF::flame;
```

## Unnamed Namespaces

You can create an unnamed namespace by omitting the namespace name:

```cpp
namespace           // unnamed namespace
{
    int ice;
    int bandycroot;
}
```

This code behaves as if it were followed by a using directive; that is, the names declared in this namespace are in potential scope until the end of the declarative region that contains the unnamed namespace. In this respect, names in an unnamed namespace are like global variables. However, if a namespace has no name, you can't explicitly use a using directive or using declaration to make the names available elsewhere. In particular, you can’t use names from an unnamed namespace in a file other than the one that contains the namespace declaration. This provides an alternative to using static variables with internal linkage. Suppose, for example, you have this code:

```cpp
static int counts;   // static storage, internal linkage
int other();
int main()
{
...
}
```

```cpp
int other()
{
...
}
```

The namespace approach is to do this instead:

```cpp
namespace
{
    int counts;   // static storage, internal linkage
}
int other();
int main()
{
...
}
```

```cpp
int other()
{
...
}
```

## A Namespace Example

Let’s take a look at a multifile example that demonstrates some of the features of namespaces. The first file in this example (see Listing 9.11) is a header file that contains some items normally found in header files—constants, structure definitions, and function prototypes. In this case, the items are placed in two namespaces. The first namespace, pers, contains a definition of a Person structure, plus prototypes for a function that fills a structure with a person’s name and a function that displays the structure’s contents. The second namespace, debts, defines a structure for storing the name of a person and the amount of money owed to that person. This structure uses the Person structure, so the debts namespace has a using directive to make the names in the pers namespace available in the debts namespace. The debts namespace also contains some prototypes.

### Listing 9.11: namesp.h

```cpp
// namesp.h
#include <string>
// create the pers and debts namespaces
namespace pers
{
    struct Person
    {
        std::string fname;
        std::string lname;
    };
    void getPerson(Person &);
    void showPerson(const Person &);

}

namespace debts
{
    using namespace pers;
    struct Debt
    {
        Person name;
        double amount;
    };
    void getDebt(Debt &);
    void showDebt(const Debt &);
    double sumDebts(const Debt ar[], int n);
}
```

### Listing 9.12: namesp.cpp

```cpp
// namesp.cpp -- namespaces
#include <iostream>
#include "namesp.h"

namespace pers
{
```
