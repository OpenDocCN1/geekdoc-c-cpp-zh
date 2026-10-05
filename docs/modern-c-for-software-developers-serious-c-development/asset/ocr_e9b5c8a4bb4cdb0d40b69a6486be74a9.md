being made.

# Overloading Function Templates

We can overload a function template with respect to the number of function parameters:

```
// Overload a function template declaration
#include <iostream>
using namespace std;

// The first overloaded version of the func() template.
template <class Ttype>
void func(Ttype a)
{
    cout << "Inside func(Ttype a)";
}

// The second overloaded version of the func() template.
template <class Ttype1, class Ttype2>
void func(Ttype1 a, Ttype2 b)
{
    cout << "Inside func(Ttype1 a, Ttype2 b)";
}
```

```
int main()
{
    func(10);      // calls func(X)
    func(10, 20);  // calls func(X, Y)
    return 0;
}
```

```
// output
Inside func(Ttype a)
Inside func(Ttype1 a, Ttype2 b)
```

# Using Ordinary Parameters With Function Templates

We can mix ordinary parameters with generic parameters in a function template:

```
// Using ordinary parameters in a function template
#include <iostream>
using namespace std;
```

```
template<class Ttype>
void print(Ttype data, int val)
```