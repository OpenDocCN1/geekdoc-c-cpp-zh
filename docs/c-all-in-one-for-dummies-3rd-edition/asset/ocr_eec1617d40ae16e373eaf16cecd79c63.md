```
```cpp
    int Weight;
    int NumberOfTeeth;
};
class Cattle {
public:
    int Weight;
    int NumberOfChildren;
};
}
```
```

The names Oxen and Cattle are unique within the Menagerie namespace. You are free to reuse these names in other namespaces without worrying about a clash. Then, if you want to use either of the two classes inside the Menagerie namespace, you would *fully qualify* the names of the classes, like so (notice the use of the double colons between Menagerie and Cattle):

```
```cpp
Menagerie::Cattle bessie;
bessie.Weight = 643;
```
```

![](bbox=[0.142, 0.383, 0.228, 0.454])

Unlike class and structure declarations, a namespace declaration doesn’t have to end with a semicolon.

If you plan to use the names in the Menagerie namespace without having to retype the namespace name each time, just put a line after the namespace declaration (but somewhere preceding the use of the names Cattle and Oxen in your code), like this:

```
```cpp
using namespace Menagerie;
```
```

Then you can access the names as if they’re not in a namespace:

```
```cpp
Cattle bessie;
bessie.Weight = 643;
```
```

![](bbox=[0.142, 0.648, 0.228, 0.724])

When you include a line that has using namespace, the compiler knows the namespace is only for lines that follow the using namespace declaration. Consider the following code:

```
```cpp
void cattleranch()
{
    Cattle x;
}
```
```

```
```cpp
using namespace Menagerie;
```
```

```
```cpp
void dairy()
{
    Cattle x;
}
```
```