
## 16 · More about Functions

Let’s analyze the call of `f(2, 3, 4, "tl1")` to understand it better. `T` becomes `int` and `val` equals 2. The other two types remain in `T_List` and the values in `v_list()` display 2 and we have the recursive call of `f(3, 4, "tl1")`. That is, each time, the `v_list` argument is replaced with the remaining values. Now `T` becomes `double` and `val` equals 3. The last type remains in `T_List` and in `v_list()` `f` displays 3.4 and the next recursive call is `f("tl1")`. Now `T` becomes `const char` and `val` equals 1. `f("tl1")` because `v_list` is empty, since there are no more arguments, and the first version of `f()` is called, which changes line and the recursion ends. To sum up, the program displays:

- 2 3.4 tl1
- 2 t3

In our example, the values in `f()` are passed by value. If we want to pass arguments of larger size (classes), then it is more efficient to use const references. For example, the declaration of `f()` becomes:

```cpp
template <typename T, typename... T_List>
void f(const T& val, const T_List&... v_list)
```

If we want to know how many types are in the list we can use the `sizeof ...` operator. For example:

```cpp
template <typename T, typename... T_List>
void f(T val, T_List... v_list)
{
    std::cout << sizeof...(T_List) << ' ' << sizeof...(v_list) << ' ' << '\n';
    f(v_list...);
}
```

`f(2, 3, 4, "tl1");` /* The first call of f() displays 2 2, the next 1 1, and the last 0 0. */

Because of their flexibility to accept an arbitrary number of arguments of any type, variadic templates are used in the standard library.
C++17 provides the ability to capture the result of using a binary operator over all the elements of a parameter pack. For example:

```cpp
template <typename... T_List>
auto sum(T_List... args)
{
    return (... + args);
}
```

The function returns the sum of all arguments. For example, if we write `sum(1, 2, 3);` the function returns their sum, that is, 6. The return statement is called a fold expression. Since three values are passed, the expression `(... + args)` expands to: `((arg1 + arg2) + arg3)`. This is called right fold.

Alternatively, we use the left fold: `return (args + ...);` which expands to: `(arg1 + (arg2 + arg3))`.

C++17 introduced the fold expressions to simplify the implementation of variadic templates.

## 502 Introduction to C++

Before we continue with the exercises I'd like to remind you something that I had written in Chapter I, yes, that was hard enough to pay attention. Now that we have come a long way and things are getting harder and harder (this chapter was really difficult), I think you will give it the proper attention. In addition to error messages, the compiler may issue warnings to the programmer about potential malfunction of the program. Although a program that issues only warning messages can be compiled, always check them and fix them if needed in order to avoid problematic situations. In fact, for better control of your program and greater security, I suggest that you set the warning level at the maximum level supported by your compiler in order to catch all of them.

## EXERCISES

**C.16.1** What is the output of the following program?

```cpp
#include <iostream>

void test(int *p, int &r, int a = 2);

int main() {
    int i = 10, j = 50;

    test(&i, j);
    std::cout << i << ' ' << j << '\n';
    return 0;
}

void test(int *p, int &r, int a) {
    *p = r;
    p = &r;
    r += 20;
}
```

**Answer:** When test() is called `p = &i` and `r = j`. So, the `*p = r;` makes `i` equal to 50. Then, `p` points to `j`, and `r += 20;` (corrected from OCR `*p = a;`) makes `j` equal to 70. As a result, the program displays 50 70. 

**C.16.2** Define the structure type `Student` with member name and grade. Write a function that has parameters two constant references to string objects and returns a reference to the larger one. Overload the function with another function, which takes as parameters two constant references to Student types and returns the name of the student with the better grade. Check if they are the same. Write a program that verifies the operation of the two functions.

```cpp
#include <iostream>
#include <string>
using std::cout;
using std::string;

struct Student
{
    string name;
    float grd;
};

const string& cmp(const string& a, const string& b);
string cmp(const Student& a, const Student& b);

int main()
{
    string s1 = "alpha", s2 = "beta";
    Student st1 = {"N.Smith", 6.5}, st2 = {"P.Krow", 5.2};

    string tmp = cmp(s1, s2); // To see that we can assign the return value to a simple variable.
    cout << tmp << '\n';

    tmp = cmp(st1, st2);
    if(tmp == "")
        cout << "Same grades\n";
    else
        cout << tmp << '\n';
    return 0;
}

const string& cmp(const string& a, const string& b)
{
    if (a > b)
        return a;
    else
        return b;
}

string cmp(const Student& a, const Student& b)
{
    if(a.grd > b.grd)
        return a.name;
    else if(a.grd < b.grd)
        return b.name;
    else
        return "";
}
```

**C.16.3** What is the output of the following program?

```cpp
#include <iostream>
#include <string>
using namespace std;

void test(int *p, int &r, int a = 2);

int main() {
    int i = 10, j = 50;
    test(&i, j);
    cout << i << ' ' << j << endl;
    return 0;
}

void test(int *p, int &r, int a) {
    *p = r;
    p = &r;
    r += 20;
}
```

**C.16.4** What is the output of the following program?

```cpp
#include <iostream>
#include <string>
using namespace std;

void test(int *p, int &r);

int main() {
    int i = 10, j = 50;
    test(&i, j);
    cout << i << ' ' << j << endl;
    return 0;
}

void test(int *p, int &r) {
    *p = r;
    r += 20;
}
```

**C.16.5** Write a function template that takes three numeric values of the same generic type and returns the value of the pair with the largest sum. For example, if the values are 3, 1, 2 the function should return 5. Overload the function with another function template with a void return type, which takes as parameter an array of generic type and returns the maximum and minimum value of the array through reference parameters of generic type. Write a program that verifies the operation of the two functions.
