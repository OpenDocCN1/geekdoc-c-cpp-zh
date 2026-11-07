```
```cpp
// Fig. 6.24: fig06_24.cpp
// Name mangling to enable type-safe linkage.

// function square for int values
int square( int x )
{
    return x * x;
} // end function square

// function square for double values
double square( double y )
{
    return y * y;
} // end function square

// function that receives arguments of types
// int, float, char and int &
void nothing1( int a, float b, char c, int &d )
{
    // empty function body
} // end function nothing1

// function that receives arguments of types
// char, int, float & and double &
int nothing2( char a, int b, float &c, double &d )
{
    return 0;
} // end function nothing2

int main()
{
} // end of main

_Z6squarei
_Z6squared
_Z8nothing1fciRi
_Z8nothing2ciRfRd
main
```
```

**Fig. 6.24** | Name mangling to enable type-safe linkage.

The compiler uses only the parameter lists to distinguish between overloaded functions. Such functions *need not* have the same number of parameters. Use caution when overloading functions with default parameters, because this may cause ambiguity.

![](bbox=[0.129, 0.82, 0.193, 0.864])

> > **Common Programming Error 6.11**
> >
> > A function with default arguments omitted might be called identically to another overloaded function; this is a compilation error. For example, having a program that contains both a function that explicitly takes no arguments and a function of the same name that contains all default arguments results in a compilation error when an attempt is made to use that function name in a call passing no arguments. The compiler cannot determine which version of the function to choose.