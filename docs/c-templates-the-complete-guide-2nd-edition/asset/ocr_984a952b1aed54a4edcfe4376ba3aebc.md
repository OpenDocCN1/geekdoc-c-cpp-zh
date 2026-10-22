it can be used to distinguish behavior for all of these three cases.
This gives the impression that declaring a parameter as a forwarding reference is almost perfect. But beware, there is no free lunch.
For example, this is the only case where the template parameter T implicitly can become a reference type. As a consequence, it might become an error to use T to declare a local object without initialization: [Click here to view code image](#)

```
template<typename T>
void passR(T&& arg) { // arg is a forwarding reference
    T x; // for passed lvalues, x is a reference, which requires an
         // initializer
    …
}

foo(42); // OK: T deduced as int
int i;
foo(i); // ERROR: T deduced as int&, which makes the declaration of x
        // in passR() invalid
```

See Section 15.6.2 on page 279 for further details about how you can deal with this situation.

# 7.3 Using std::ref() and std::cref()

Since C++11, you can let the caller decide, for a function template argument, whether to pass it by value or by reference. When a template is declared to take arguments by value, the caller can use `std::cref()` and `std::ref()`, declared in header file `<functional>`, to pass the argument by reference. For example: [Click here to view code image](#)

```
template<typename T>
void printT (T arg) {
    …
}

std::string s = "hello";
printT(s); // pass by reference
printT(std::cref(s)); // pass s “as if by reference”
```

However, note that `std::cref()` does not change the handling of parameters in templates. Instead, it uses a trick: It wraps the passed argument s by an object that acts like a reference. In fact, it creates an object of type `std::reference_wrapper<>` referring to the original argument and