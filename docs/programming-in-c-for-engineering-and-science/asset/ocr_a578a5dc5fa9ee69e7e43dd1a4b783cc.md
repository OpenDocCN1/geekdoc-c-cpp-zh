# 10.6.2.1 Signatures

The **signature** of a function is a list of the types of its parameters, including any const and reference parameter indicators (&). For example, the signature of the polarToRectangular() function in Example 10.2 is

```
(double, double, double &, double &)
```

and the signature of the makeChange() function in Example 10.3 is

```
(double, double, int &, int &, int &, int &, int &)
```

while the signature of the chopIPAddress function in Example 10.5 is

```
(const string &, string &, string &, string &, string &)
```

Signatures are important, because the compiler essentially considers a function’s signature to be part of its name.

# 10.6.2.2 Function Overloading

If two different functions have the same name, that name is said to be **overloaded**. For example, when we use the same name for both of the summation functions,

```
int sum(int n)
{
    return n * (n + 1) / 2;
}
```

```
int sum(int m, int n)
{
    assert(m < n);
    return (n - m + 1) * (n + m) / 2;
}
```

we are overloading the name sum with two different definitions. The compiler is able to distinguish them from one another, because they have different signatures. If we call sum() with

```
cout << sum(100) << endl;
```

the call has one int argument, and so the compiler associates this call with the first definition of sum() whose signature has one int type. However, if we write

```
cout << sum(20, 40) << endl;
```

the function call has two int arguments, and so the compiler associates this call with the second definition of sum() whose signature has two int types.

Signatures thus allow the C++ compiler to distinguish calls to different functions with the same name. As a result, we have the following rule governing overloading: *The name of a function can be overloaded, provided no two versions of the function have the same signature.* Note that the return type of a function is not a part of its signature. Thus, two functions with identical signatures but with different return types cannot have the same name.