```
```cpp
template <class T, int n>
T & Array<T,n>::operator[] (int i)
{
    if (i < 0 || i >= n)
    {
        std::cerr << "Error in array limits: " << i
                  << " is out of range\n";
        std::exit(EXIT_FAILURE);
    }
    return ar[i];
}

template <class T, int n>
T Array<T,n>::operator[] (int i) const
{
    if (i < 0 || i >= n)
    {
        std::cerr << "Error in array limits: " << i
                  << " is out of range\n";
        std::exit(EXIT_FAILURE);
    }
    return ar[i];
}

#endif
```
```

Note the template heading in Listing 14.17:

```
```cpp
template <class T, int n>
```
```

The keyword class (or, equivalently in this context, typename) identifies T as a type parameter, or type argument. int identifies n as being an int type. This second kind of parameter, one that specifies a particular type instead of acting as a generic name for a type, is called a non-type, or expression, argument. Suppose you have the following declaration:

```
```cpp
ArrayTP<double, 12> eggweights;
```
```

This causes the compiler to define a class called ArrayTP<double,12> and to create an eggweights object of that class. When defining the class, the compiler replaces T with double and n with 12.

Expression arguments have some restrictions. An expression argument can be an integer type, an enumeration type, a reference, or a pointer. Thus, double m is ruled out, but double & rm and double * pm are allowed. Also the template code can't alter the value of the argument or take its address. Thus, in the ArrayTP template, expressions such as n++ or &n would not be allowed. Also when you instantiate a template, the value used for the expression argument should be a constant expression.