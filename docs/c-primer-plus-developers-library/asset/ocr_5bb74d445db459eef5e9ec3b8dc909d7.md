The C++ approach of using the keyword inline to identify inline functions is much more dependable because it uses true argument passing. Furthermore, C++ inline functions can be regular functions or class methods.

```
```cpp
class dormant
{
private:
    int period;
    ...
public:
    int Period() const { return period; }  // automatically inline
    ...
};
```
```

One positive feature of the #define macro is that it is typeless, so it can be used with any type for which the operation makes sense. In C++ you can create inline templates to achieve type-independent functions while retaining argument passing.

In short, you should use C++ inline instead of C #define macros.

# ## Use Function Prototypes

Actually, you don't have a choice: Although prototyping is optional in C, it is mandatory in C++. Note that a function that is defined before its first use, such as an inline function, serves as its own prototype.

You should use const in function prototypes and headers when appropriate. In particular, you should use const with pointer parameters and reference parameters representing data that is not to be altered. Not only does this allow the compiler to catch errors that change data, it also makes a function more general. That is, a function with a const pointer or reference can process both const and non-const data, whereas a function that fails to use const with a pointer or reference can process only non-const.

# ## Use Type Casts

One of Stroustrup's pet peeves about C is its undisciplined type cast operator. True, type casts are often necessary, but the standard type cast is too unrestrictive. For example, consider the following code:

```
```cpp
struct Doof
{
    double feeb;
    double steeb;
    char sgif[10];
};
Doof leam;
short * ps = (short *) & leam;  // old syntax
int * pi = int * (&leam);       // new syntax
```
```