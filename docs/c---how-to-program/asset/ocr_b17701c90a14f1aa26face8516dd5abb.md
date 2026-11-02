Figure 15.11 was compiled with GNU C++. Rather than showing the execution output of the program (as we normally would), we show the mangled function names produced in assembly language by GNU C++. Each mangled name (other than main) begins with two underscores (__) followed by the letter Z, a number and the function name. The number that follows Z specifies how many characters are in the function's name. For example, function square has 6 characters in its name, so its mangled name is prefixed with __Z6.

> **Common Programming Error 15.9**
> 
> *Creating overloaded functions with identical parameter lists and different return types is a compilation error.*

```
// Fig. 15.11: fig15_11.cpp
// Name mangling to enable type-safe linkage.

// function square for int values
int square( int x )
{
    return x * x;
}

// function square for double values
double square( double y )
{
    return y * y;
}

// function that receives arguments of types
// int, float, char and int &
void nothing1( int a, float b, char c, int &d )
{
    // empty function body
}

// function that receives arguments of types
// char, int, float & and double &
int nothing2( char a, int b, float &c, double &d )
{
    return 0;
}

int main()
{
    return 0; // indicates successful termination
}
```

```
__Z6squarei
__Z6squared
__Z8nothing1fcRi
__Z8nothing2ciRFkd
__main
```

Fig. 15.11 | Name mangling to enable type-safe linkage.