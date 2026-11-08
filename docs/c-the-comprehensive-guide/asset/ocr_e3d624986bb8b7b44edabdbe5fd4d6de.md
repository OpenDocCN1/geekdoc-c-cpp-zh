# 23.1.2  A Type as Parameter

If you write it in such a way that the type is also flexible, it looks like this:

```
template<typename TYPE>
void print(TYPE value) {
    cout << value;
}
```

One could say the function now has two parameters: TYPE for the type of the argument and value for its value.

When calling it specifically, you now need to specify both things. As such, you write the type argument after the function name in angle brackets:

```
print<int>(5);
print<double>(-10.25);
print<const char*>("Flamingo");
```

But the compiler already knows that 5 is an int, -10.25 is a double, and "Flamingo" is a const char*. And when the compiler can make the choice for you, you can also omit the angle brackets and the explicit type when calling this function:

```
print(5);
print(-10.25);
print("Flamingo");
```

These lines are equivalent to the previous example. However, it is important to note that you now actually have three functions: one for int as a parameter, one for double, and one for const char*.

Note that whether you write `template<typename TYPE>` or `template<class TYPE>` is irrelevant. Both notations are equivalent, and it is a matter of taste or agreement to use one or the other. The standard library prefers class here, while I personally prefer typename.

# 23.1.3  Function Body of a Function Template

The function body of print takes advantage of the fact that the output operator operator<< is defined for int, double, and const char*. This is, of course, not true for all types.

```
// https://godbolt.org/z/aMP3jK7EE
#include <iostream>
struct Number {
    int value;
};
template<typename TYPE>
void print(TYPE value) {
    std::cout << value << "\n";
}
```