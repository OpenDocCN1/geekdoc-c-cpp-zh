```
```cpp
// function square for double values
double square( double y )
{
    return y * y;
} // end function square

// function that receives arguments of types
// int, float, char and int &
void nothing1( int a, float b, char c, int & )
{
    // empty function body
} // end function nothing1

// function that receives arguments of types
// char, int, float and double &
int nothing2( char a, int b, float &, double & )
{
    return 0;
} // end function nothing2

int main()
{
} // end main
```
```

```
```text
_Z6squarei
_Z6squared
_Z8nothing1ifcRi
_Z8nothing2icfRd
_main
```
```

**Fig. 6.25** | Name mangling to enable type-safe linkage. (Part 2 of 2.)

![](bbox=[0.16, 0.62, 0.216, 0.657])

> **Common Programming Error 6.14**
> 
> Creating overloaded functions with identical parameter lists and different return types is a compilation error.

The compiler uses only the parameter lists to distinguish between overloaded functions. Such functions need not have the same number of parameters. Use caution when overloading functions with default parameters, because this may cause ambiguity.

![](bbox=[0.16, 0.756, 0.216, 0.795])

> **Common Programming Error 6.15**
> 
> A function with default arguments omitted might be called identically to another overloaded function; this is a compilation error. For example, having a program that contains both a function that explicitly takes no arguments and a function of the same name that contains a default arguments results in a compilation error when an attempt is made to use that function name in a call passing no arguments. The compiler does not know which version of the function to choose.

# Overloaded Operators

In Chapter 11, we discuss how to overload operators to define how they should operate on objects of user-defined data types. (In fact, we’ve been using many overloaded operators