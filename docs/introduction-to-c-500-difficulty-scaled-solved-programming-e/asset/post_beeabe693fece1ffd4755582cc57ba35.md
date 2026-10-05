
[content]
# 11 • Functions 327

To handle the optional argument list, we use a set of macros defined in the cstdarg library. Macros are discussed in Chapter 15. For now, assume that their behaviour is similar to functions.

- va_list: A variable of type va_list is used to point to the optional argument list.
- va_start(): The va_start() macro takes two parameters. The first one is of type va_list, and the second one should be the name of the last parameter. For example, the last fixed parameter in test() is va_start() sets the va_list to point to the first optional argument. va_start() must be called before va_arg() is used for first time.
- va_arg(): The va_arg() macro takes two parameters. The first one is of type va_list and the second one is type of an optional argument. For example, the first optional argument is int. The va_list must be initialized with va_start(). va_arg() returns the value of the optional argument and advances the va_list to point to the next optional argument. Therefore, in order to get the values of all optional arguments, we should call va_arg() as many times as the number of optional arguments.
- va_end(): The va_end() macro takes one parameter of type va_list. It must be called to end the processing of the optional argument list.

In the following program, test() takes a variable number of parameters of type char*. The fixed parameter num identifies them.

```cpp
#include <iostream> // Example 11.28
#include <cstdarg>

void test(int num, ...);

int main() 
{
    test(3, "t1", "t2", "t3");
    return 0;
}

void test(int num) {
    char *str;
    int i;
    va_list arg_ptr;

    va_start(arg_ptr, num); /* va_start() initializes the va_list variable. In particular, arg_ptr points to the first optional argument.
    Notice that the name of the second argument should be the same with the name of the last fixed parameter in the definition of test(). */
    for(i = 0; i < num; i++) {
        str = va_arg(arg_ptr, char*); /* Each call of va_arg() returns the value of the respective optional argument of type char* and arg_ptr advances to point to the next optional argument. The second argument is char, because it is said that the type of all optional arguments is char*. */
        std::cout << str << " '";
    }
    va_end(arg_ptr);
}
```

The program outputs the values of the optional arguments: t1 t2 t3

# 328 Introduction to C++

The primary difficulty in using a function with a variable argument list is that there is no easy way to determine the number and types of its optional arguments. To find the number, a simple solution is to add a fixed parameter, which declares that number. In the previous example, we used the parameter num. If the arguments are all of the same type, we could use a special value to mark the end of the list. Moreover, the function must somehow be informed about their types. For example, for those who know from C the printf() and scanf() functions, they use the format string to get the necessary type information to process the argument list. In general, ellipsis (...) comes from C, it should be used with types that are common in C and C++ and should not be used with other types.

# EXERCISE

C11.28 Write a function that takes a variable parameter list of type double and returns the largest value. Write a program that reads three floats and uses the function to display the largest value.

```cpp
#include <iostream>
#include <cstdarg>

double find_max(int num, ...);

int main() {
    double i, j, k;

    std::cout << "Enter numbers: ";
    std::cin >> i >> j >> k;

    std::cout << "Max = " << find_max(3, i, j, k) << '\n';
    return 0;
}

double find_max(int num, ...) {
    int i;
    double max, tmp;
    va_list arg_ptr;

    va_start(arg_ptr, num);
    max = va_arg(arg_ptr, double);
    for (i = 1; i < num; i++) {
        tmp = va_arg(arg_ptr, double);
        if (max < tmp)
            max = tmp;
    }
    va_end(arg_ptr);
    return max;
}
```

**Comments:** Note that we can use find_max() to find the largest of any number of double arguments, not just 3.

With the C++11 standard we can write a function that accepts a variable number of arguments of a particular type using the standard library initializer_list. This type is defined in the initializer_list file and represents an array. As with the vector type when declaring an initializer_list we need to specify the type of elements. The elements of the initializer_list are const, so we cannot change their values. Also, it supports begin() and end() functions, similar to those of vector, to access its elements. Let's look at an example:

```cpp
#include <iostream> // Example 11.29
#include <initializer_list>
using namespace std;

template <typename T> void show(const initializer_list<T>& lst);

int main() {
    initializer_list<string> str_lst("t1", "t2", "t3");
    show(str_lst);
    show("t1", "t2", "t3"); /* When passing a list of values to an
    initializer_list parameter, the list must be enclosed in braces. */
    initializer_list<int> int_lst(1, 2, 3);
    show(int_lst);
    show(1, 2, 3);
    return 0;
}

template <typename T> void show(const initializer_list<T>& lst) {
    for (auto cur = lst.begin(); cur != lst.end(); ++cur)
        std::cout << *cur << ' ';
}
```

The program uses the template show() to display the elements contained in the initializer_list parameter. You'll see how it works when we discuss templates in Chapter 16. For now, it is enough to know that the type T for the str_lst variable will be replaced with string and for int_lst with int. As the comment says, when passing a list of values to an initializer_list it must be enclosed in braces. Finally, the program displays:

```
t1 t2 t3
t1 t2 t3
1 2 3
1 2 3
```

Note that a function with an initializer_list parameter can accept additional ordinary parameters as well. For example:

```cpp
void f(const initializer_list<int>& lst, double d); /* f() accepts an
initializer_list parameter that contains integers and a double value. */
```

and an example of how to call it: f({1, 2}, 3.4);

# RECURSIVE FUNCTIONS

A function that calls itself is recursive. For example:

```cpp
#include <iostream> // Example 11.30

void show(int num);

int main() {
    int i;
    std::cout << "Enter number: ";
    std::cin >> i;
    show(i);
    return 0;
}

void show(int num) {
    if(num > 0)
        show(num - 1);
    std::cout << num << "\n";
}
```
[/content]
