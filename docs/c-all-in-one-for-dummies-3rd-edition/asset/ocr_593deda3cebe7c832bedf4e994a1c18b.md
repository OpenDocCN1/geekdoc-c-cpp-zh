when a function takes a pointer or reference to a class, you can instead pass an instance of a derived class.)

# **Deriving a class template from a class template**

If you have a class template and you want to derive another class template from it, first you need to think about exactly what you're doing. Not like what you're doing spending all your days programming when you could be out enjoying the sunshine; rather, what we mean is, "What process takes place when you attempt to derive a class template from another class template?"

Remember that a class template isn't a class: A class template is a cookie-cutter that the compiler uses to build a class. If, in a derivation, the base class and the derived classes are both templates, what you really have is the following:

+   1. The first class is a template from which the compiler builds classes.
+   2. The second class is a template from which the compiler will build classes that are derived from classes built from the first template.

Now think about this: You create a class based on the base class template. Then you create a second class based on the second template. Does this automatically mean that the second class is derived from the first class? Nope! Here's why: From the first template, you can create many classes. Now if you create a class from the second template, which of those many classes will it be derived from?

To understand what's happening here, take a look at the TemplateFrom Template example shown in Listing 5-8. To keep the code simple, we put the jokes aside and just gave the identifiers basic names. (And notice that we commented one of the lines out. If you're typing this, go ahead and type that line in, too, with the comment slashes, because we want you to try something in a moment.)

# **Listing 5-8: Deriving a Class Template from a Class Template**

```
~~~cpp
#include <iostream>

using namespace std;

template <typename T>
class Base
{
public:
    T a;
};

template <typename T>
~~~
```