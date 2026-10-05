# Introduction to C++

```
do_swap(i, j); // Call the explicitly instantiated version.
do_swap(k, m); // Call the function template.
do_swap(s1, s2); // Call the specialized version.
...
return 0;

```

When the compiler encounters the do_swap() declaration for the int type, it creates instantly an int version of the do_swap(). In main(), the compiler checks the do_swap() arguments and the value to val. the appropriate version. For example, the first call it calls the int version that has already been created, in the second call it creates a double version, and in the third call it selects the specialized version for the Student type.

# Templates with Variable Number of Types

C11 allows you to define a function template that accepts a variable number of parameters of any type. This is called a variadic template. Let's look at an example:

```
#include <iostream> // Example 16.17

void f() { std::cout << '\n'; }

template <typename T, typename... T_List>
void f(T val, T_List... v_list)
{
    std::cout << val << ' ';
    f(v_list...);
}

int main() {
    f(2, 3.4, "t1");
    f("t2", "t3");
    return 0;
}
```

In the second version of f() in order to declare that the second parameter accepts a variable number of types we add after the word typename. As for the name (e.g., T, T_List) you can choose any valid name to use. Thus, T_List contains a list of types, while T corresponds to a single type. We are also added after the name in the parameter v_list is a list of lists that matches the match list in T_List, while val corresponds to a single value of T.

So, when f() is called, the T_List parameter contains all the types that match the arguments, that is, int, double, and const char*. The v_list parameter contains the values 2, 3.4, and t1. Similarly, in the second call, T_List contains two types of const char* and the values t2 and t3.

Fine, and how does f() access the values? Note that we cannot index v_list, that is like v[list] to display the value. Access is achieved through recursion. In particular, each time f() is called the type of the first argument is assigned to T and the value to val. The remaining types remain in T_List and v_list will be accessed, one at a time, with the next recursive calls of f() until the list of arguments is exhausted. Then, the first version of f() will be called. This is the reason for its existence, so the recursion ends. In example, it changes line so that the arguments of the second f() appear on the next line. Note that in the f() call we add ... after the name of the argument, to expand the list of values contained in v_list.