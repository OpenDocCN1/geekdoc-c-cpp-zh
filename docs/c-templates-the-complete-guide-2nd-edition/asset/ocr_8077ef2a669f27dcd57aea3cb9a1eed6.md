const and volatile qualifiers, is equivalent to std::initializer_list<P'> for some type P' that has a deducible pattern, deduction proceeds by comparing P' to the type of each element in the initializer list, succeeding only if all of the elements have the same type: Click here to view code image

# deduce/initlist.cpp

```
#include <initializer_list>

template<typename T> void f(std::initializer_list<T>);

int main()
{
f({2, 3, 5, 7, 9}); // OK: T is deduced to int
f({'a', 'e', 'i', 'o', 'u', 42}); //ERROR: T deduced to both char and int
}
```

Similarly, if the parameter type P is a reference to an array type with element type P' for some type P' that has a deducible pattern, deduction proceeds by comparing P' to the type of each element in the initializer list, succeeding only if all of the elements have the same type. Furthermore, if the bound has a deducible pattern (i.e., just names a nontype template parameter), then that bound is deduced to the number of elements in the list.

# 15.5 Parameter Packs

The deduction process matches each argument to each parameter to determine the values of template arguments. When performing template argument deduction for variadic templates, however, the 1:1 relationship between parameters and arguments no longer holds, because a parameter pack can match multiple arguments. In this case, the same parameter pack (P) is matched to multiple arguments (A), and each matching produces additional values for any template parameter packs in P: Click here to view code image

```
template<typename First, typename... Rest>
void f(First first, Rest... rest);

void g(int i, double j, int* k)
{
f(i, j, k); // deduces First to int, Rest to {double, int*}
```