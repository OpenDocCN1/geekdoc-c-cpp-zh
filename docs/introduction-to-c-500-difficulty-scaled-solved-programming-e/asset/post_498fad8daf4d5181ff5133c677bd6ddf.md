
prototypes are missing and i has been declared as bool? The compiler converts i to double and selects t first f() again. The process to decide which function to use when there are many candidates is called overload resolution. A detailed discussion is out of scope of this book. In short, ranking from best to worst that the compiler applies to the most suitable function is:

- Exact match of arguments.
- Match using integral promotions as we saw in Chapter 2 (e.g., short to int) and float to double.
- Match using standard conventions (e.g., int to double).

If there are more than one “best”, the compiler rejects the call as ambiguous.
Note that the compiler distinguishes between const and non-const for reference and pointers. For example:

```
void f(const char *a);
void f(char *a);
```

Suppose we write:

```
const char s1[] = "text";
char s2[] = "text";
f(s1); // f(const char *a);
f(s2); // f(char *a);
```

In the first call of f() the compiler selects the first version and in the second call selects the second version. Note that in the second call, since a non-const argument can be passed to const both versions are candidates, but the compiler selects the second version because it matches exactly.

## FUNCTION TEMPLATES

Function templates, why do we need them, are they important? No doubt, templates are the basis for generic programming, that is, to write code that can work with a variety of types. It is an easy section to read? I'd not say. Still difficult to learn? Yes, and more on the way. I know, that's a lot of new stuff, we have a break with More from Sisters of Mercy and prepare yourself to explore this very interesting feature.

A function template allows us to define a function in terms of a generic type(s) so that it can handle different types of data. Each time such a function is called, the compiler checks the type of the arguments and creates a version of the function for particular types. An example of defining a function template:

```
template <typename type1, typename type2, ...>
return_type function_name(parameter_list)
```

Let's see how it works. Suppose that we want to create a function that returns the absolute value of a number. Since we do not know the type of the number we have to write different functions or overload one function for all possible types. We now have the flexibility that the templates provide. With templates we do not need to write different versions; we just write a function template in terms of some generic type and that same function can work for a variety of types. This is the concept of generic programming.

The following program uses the template abs() function to find the absolute value of numbers with different types:

```cpp
#include <iostream> // Example 16.11

template <typename T> T abs(T a);
int main() {
    int a = -6;
    float b = -1.2;
    double c = 3.4;

    std::cout << abs(a) << ' ' << abs(b) << ' ' << abs(c) << '\n';
    return 0;
}

template <typename T> T abs(T a) {
    T k;
    if(a < 0)
        k = -a;
    else
        k = a;
    return k;
}
```

Regarding the program design, in a project with multiple source files that may use the same template, the common practice is to put the definition of a function template in a header file and include that file in any file that uses the template. Unlike our examples which consist of a single source file, for simplicity, I'll put the declaration and definition of the function template in that.

To declare a function template we write the keyword template and inside <> the keyword typename and the name of the template parameters. Unlike the parameters of an ordinary function which are used to pass values, the parameters of a function template are typically used to pass types. Note that we can also use the class instead of the word typename. The word typename was later added to C++, so you may run inside code that uses the word class. My preference is to use typename, because it makes clear that the T parameter corresponds to the name of some type. Also the word class may create the false impression that the type must be a class, which is not true. Any names as long as they follow the naming rules. The common practice is to use short names that begin with the letter T (or T1, T2).

The template is not a function definition. It is just a blueprint that provides the directions to how to implement the function. So when the function is created? Each time the compiler encounters a call to abs() it replaces the T with the type of the argument and creates the function. This is referred to as template argument deduction. For example, in the first call, it replaces the T with int and creates an int version of the function. So, the resulting definition is:

```cpp
int abs(int a) {
    int k;
    if(a < 0)
        k = -a;
    else
        k = a;
    return k;
}
```

Similarly, in the second call, the compiler replaces the T type with float and the definition of the resulting float version is:

```cpp
float abs(float a)
{
    float k;

    if(a < 0)
        k = -a;
    else
        k = a;
    return k;
}
```

The compiler creates a definition of the function template only if it is used in the program. If not used, it will not be defined.

So, we see that in each call the compiler checks the type of the argument; it replaces each appearance of the generic type with it and creates the corresponding version. This type of instantiation is implicit instantiation, in the sense that the compiler creates the function when it encounters the call and defines the type of the passed arguments. If another function requires the same instance, the compiler uses the existing instance.

Since the type of the arguments is fixed and known, the compiler instantiates templates at compile time. So, as with function overloading, the polymorphism is achieved at compile time, which means that the use of templates does not induce a delay in the execution time of the program. In other words, templates provide complete type polymorphism. Finally, the programs: we could omit the declaration of k and write abs() as follows:

```cpp
if(a < 0)
    return -a;
else
    return a; a < 0 ? -a : a;
```

The reason I used k is to show that templates can apply to generic types. Note that the use of templates does not make the executable larger. For example, we can use templates for different types. Regarding the parameters of a function template, not of them have to be generic. We can mix them with specific types. Here is an example:

```cpp
template <typename T> void f(T a, int b)
```

Like an ordinary function, a template can be declared as inline or constexpr. The specifier is added after the return type. For example:

```cpp
inline <typename T> T abs(T a); // Wrong.
template <typename T> inline abs(T a); // Correct.
```

## Templated Variables

C++14 allows the creation of templated variables. For example:

```cpp
template <typename T> T pi = T(3.14159265359);
```

Typically, a templated variable is used in function templates and classes. For example:

```cpp
template <typename T>
circle_perim 2*rad*pi<T>; {
    return;
}
```

The idea behind the templated variables is, instead of having different variables and initializing expressions for the respective types, it is sometimes to vary the type of a variable used for generic purposes. For example, we can write:

```cpp
int rad = 5;
int per = circle_perim(rad);
```

When circle_perim() is called, the compiler replaces the T type with the type of the rad argument and creates the function. Since T becomes int, rad becomes 3 and the function returns 30.

## Errors When Using Templates

Try this exercise. Write a function template that swaps the values of its two arguments. Assume that the arguments are of the same type. Then, write a program to verify the operation of the function.

```cpp
#include <iostream> // Example 16.12
```

```cpp
template <typename T> void do_swap(T& a, T& b);
```

```cpp
int main() {
    int a = 1, b = 2;
    double c = 3.4, d = 5.6;

    do_swap(a, b);
    do_swap(c, d);
    std::cout << a << ' ' << b << ' ' << c << ' ' << d << '\n';
    return 0;
}
```
