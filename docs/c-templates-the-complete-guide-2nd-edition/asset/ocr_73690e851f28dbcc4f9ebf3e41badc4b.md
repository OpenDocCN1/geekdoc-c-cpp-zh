```
int main ()
{
int a = 7;
int b = 42;
auto m1 = ::max(a,b); // max() for two values of type int

std::string s1 = "hey"; "
std::string s2 = "you"; "
auto m2 = ::max(s1,s2); // max() for two values of type std::string

int* p1 = &b;
int* p2 = &a;
auto m3 = ::max(p1,p2); // max() for two pointers

char const* x = hello"; "
char const* y = "world"; "
auto m4 = ::max(x,y); // max() for two C-strings
}
```

Note that in all overloads of max() we pass the arguments by value. In general, it is a good idea not to change more than necessary when overloading function templates. You should limit your changes to the number of parameters or to specifying template parameters explicitly. Otherwise, unexpected effects may happen. For example, if you implement your max() template to pass the arguments by reference and overload it for two C-strings passed by value, you can’t use the three-argument version to compute the maximum of three C-strings: Click here to view code image

# basics/max3ref.cpp

```
#include <cstring>

// maximum of two values of any type (call-by-reference)
template<typename T> T const& max (T const& a, T const& b)
{
return b < a ? a : b;
}
// maximum of two C-strings (call-by-value)
char const* max (char const* a, char const* b)
{
return std::strcmp(b,a) < 0 ? a : b;
}

// maximum of three values of any type (call-by-reference)
template<typename T> T const& max (T const& a, T const& b, T const& c)
{
```