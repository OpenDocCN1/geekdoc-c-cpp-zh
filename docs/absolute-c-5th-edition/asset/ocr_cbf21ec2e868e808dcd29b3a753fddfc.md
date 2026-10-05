# CHAPTER 1 C+ Basics

# The expression

```
static_cast<double>(m)
```

is a type cast. The expression static_cast<double> is like a function that takes an int argument (actually, of almost any type) and returns an “equivalent” value of type double. So, if the value of m is 2, the expression static_cast<double>(m) returns the value 2.0.

Note that static_cast<double>(n) does not change the variable of n. If n has the value 2 this expression is evaluated, n still has the value 2 after the expression is evaluated. (If you know what a function is in mathematics or in some programming language, you can think of static_cast<double> as a function that returns an “equivalent” value of type.)

You may use any type name in place of double to obtain a cast to another type. We said this produces an “equivalent” value of the target. The word equivalent is in quotes because there is no clear notion of what applies to any two types. In the case of a cast from an integer to a floating-point type, the effect is to add a decimal point and zero. The cast in the other direction, from a floating-point type to integer, simply deletes the decimal point and all digits after the decimal point. Note that when casting from a floating-point type to an integer, the number is truncated, not rounded. static_cast<int>(2.9) is 2; it is not 3.

is the most common kind of cast and the only one we will use for some time. For completeness and reference value, we list all four kinds of casts. Some not make sense until you reach the relevant topics. If some or all of the remaining three kinds do not make sense to you at this, do not worry. The four kinds of cast are as follows:

```
static_cast<Type>(Expression)
const_cast<Type>(Expression)
dynamic_cast<Type>(Expression)
reinterpret_cast<Type>(Expression)
```

We have already discussed static_cast. It is a general-purpose type cast that applies in “ordinary” situations. The const_cast is used to cast away constancy. The dynamic_cast is used for downcasting from one type to a descendant type in an inheritance hierarchy. The reinterpret_cast is an implementation-dependent cast that we will not discuss in this book and you are unlikely to need. (These descriptions may not make sense until you cover the appropriate topics, where they will be discussed. For now, we only use static_cast.)

The older form of type casting is approximately equivalent to the static_cast kind of casting but uses a different notation. One of the two notations uses a type name as if it were a function. For example, int(9.3) returns the double(42) returns the value 42.0. The second, notation for the older form of type casting would be (double)42 instead of (double)(42). Each notation can be used with variables or other more complicated expressions instead of just constants.

Although C++ retains this older form of type casting, we are encouraged to use the newer form of type casting. (Someday, the older form may go away, although there is, as of yet, no plan for its elimination.)