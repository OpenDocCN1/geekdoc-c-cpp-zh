Go ahead and say it: “Well, this is all fine and dandy, but can you have two functions by the same name like this?” Yup! The Combine example, shown in Listing 5-10, contains the entire code. Both functions are present in the listing.

# Listing 5-10: Writing Two Versions of a Function

```
```cpp
#include <iostream>

using namespace std;

void Combine(string first, string second)
{
    cout << first << " " << second << endl;
}

void Combine(int first, int second)
{
    int sum = first + second;
    cout << first << " " << second << " " << sum << endl;
}

int main()
{
    Combine("David", "Letterman");
    Combine(15, 20);
    return 0;
}
```
```

Note in `main()` that we called each function. How did we specify which one we want? *By simply passing the right types.* Take a close look at the first call:

```
```cpp
Combine("David", "Letterman");
```
```

This call includes two strings, so the compiler knows to use the first version, which takes two strings. Now look at the second function call:

```
```cpp
Combine(15, 20);
```
```

This call takes two integers, so the compiler knows to use the second version of the function.

This process of writing two versions of the same function is called *overloading* the function. Normally, overloading is a bad thing, like when we go to a nice restaurant and overload our stomachs. But here it’s a good thing — and even useful.

When you overload a function, the parameters must differ. For example, the functions can take the same type of information but use a different number of parameters. Of course, the previous example shows that the parameters can also vary by type. You can also have different return types, though they must differ by *more than just the return type*.

![](bbox=[0.11, 0.87, 0.19, 0.94])