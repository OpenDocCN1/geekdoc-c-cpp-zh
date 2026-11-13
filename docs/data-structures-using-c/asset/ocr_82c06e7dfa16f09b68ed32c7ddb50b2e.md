Here, `ShowData()` is a member function whose code is written outside the class definition. The function `GetData()` is defined inside the class definition, and hence is considered as an inline function. If the user wishes to define a function outside the class and still wants to make it an inline function, it can be done by explicitly instructing the compiler to do so, as shown in Program Code A.7.

```
PROGRAM CODE A.7

// A sample C++ program with inline function outside class
#include<iostream.h>
class ABC
{
    int a, b, c;
    public:
        void GetData()
        {
            cin >> a >> b >> c;
        }
};

inline void ABC :: ShowData()
{
    cout << a << "\t"<< b << "\t" << c;
}
```

We have discussed that an inline function call is replaced by its code, similar to macro expansion. However, there is one major difference between an inline function and a macro. Let us consider the code in Program Code A.8.

```
PROGRAM CODE A.8

// A sample C++ program with macro and inline function
#include<iostream.h>
#define Square1(x) x * x
inline int Square2(int x)
{
    return x * x;
}
int main()
{
    cout << "\n Using macro" << Square1(5 + 5);
```