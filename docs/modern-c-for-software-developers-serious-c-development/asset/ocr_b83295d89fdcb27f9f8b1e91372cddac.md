# Modern C++: explicit Keyword (C++11)

The C++ compiler will implicitly perform type conversions when required.
example:

```
int x = 3;
float y = x + 5.5;
```

x will be automatically cast to a float data type before the addition is performed.
Implicit type conversions typically involve type widening.

We can prevent the compiler from implicitly converting a type by using the *explicit*
keyword. *explicit* is frequently used to qualify constructors. Consider the following
example:

```
class Array {
    public:
        explicit Array(size_t x);
};
```

This will prevent the implicit type conversion of the parameter x in the constructor.