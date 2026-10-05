A parameter value is considered constant within the function and we are not allowed to change its value. That is, it is error to write size = 20. We'll discuss more non-type parameters in the corresponding section in Chapter 23.

# Default Parameter Values

As ordinary functions, we can set default values to the parameters of a function template. For example:

```
template <typename T1, typename T2 = int> void f()
{
  T1 i;
  T2 j;
  ...
}
```

If the type of T2 is omitted, we write f<double>(); the type of T1 will be double and the type of T2 will be int. 
We can also specify default values for non-type parameters. For example:

```
template <typename T, int s = 20> void f(){...}
```

If we write f<int>(); the type of T will be int and s equal to 20.

# Explicit Instantiation

In addition to the implicit instantiation we can instruct the compiler to create the function definition directly. This type instantiation is called explicit instantiation. An explicit instantiation begins with the word template without the <. The types are contained inside <>. For example, if we add the statement in C.16.11:

```
template int abs<int>(int a);
```

the compiler will an instance of the abs() function to create directly a definition using the int type. Explicit instantiation also occurs if the function is used in the program. For example:

```
double c = 3.4;
cout << abs<double>(c) << '\
';
```

This creates an explicit instantiation for the double type. If the specified type does not match the type of the argument, the compiler will attempt a type conversion. For example, if we write:

```
cout << abs<int>(c) << '\n';
```

the compiler makes an instance of the int type. Thus, c is converted to int and the code outputs 3. So, be careful with type mismatches, because the compiler may provide an undesirable implicit conversion.