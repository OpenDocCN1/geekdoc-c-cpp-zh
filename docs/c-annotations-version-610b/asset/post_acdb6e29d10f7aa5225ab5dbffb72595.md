
### 2.5.3 Strict type checking

C++ uses very strict type checking. A prototype must be known for each function before it is called, and the call must match the prototype. The program

```cpp
int main()
{
    printf("Hello World\n");
}
```

often compiles under C, albeit with a warning that printf() is an unknown function. But C++ compilers (should) fail to produce code in such cases. The error is of course caused by the missing #include <stdio.h> which in C++ is more commonly included as #include <cstdio> directive.

And while we’re at it: as we’ve seen in C++ main always uses the int return value. Although it is possible to define int main() without explicitly defining a return statement, within main it is not possible to use a return statement without an explicit int-expression. For example:

```cpp
int main()
{
    return;      // won’t compile: expects int expression, e.g.
                 // return 1;
}
```

### 2.5.4 Function Overloading

In C++ it is possible to define functions having identical names but performing different actions. The functions must differ in their parameter lists (and/or in their const attribute). An example is given below:

```cpp
#include <stdio.h>

void show(int val)
{
    printf("Integer: %d\n", val);
}

void show(double val)
{
    printf("Double: %lf\n", val);
}

void show(char const *val)
{
    printf("String: %s\n", val);
}

int main()
{
    show(12);
    show(3.1415);
    show("Hello World!\n");
}
```

In the above program three functions show are defined, only differing in their parameter lists, expecting an int, double and char *, respectively. The functions have identical names. Functions having identical names but different parameter lists are called *overloaded*. The act of defining such functions is called ‘function overloading’.

The C++ compiler implements function overloading in a rather simple way. Although the functions share their names (in this example show), the compiler (and hence the linker) use quite different names. The conversion of a name in the source file to an internally used name is called ‘name mangling’. E.g., The C++ compiler might convert the prototype `void show(int);` to the internal name `Vshowi`, while an analogous function having a `char *` argument might be called `VshowCP`. The actual names that are used internally depend on the compiler and are not relevant for the programmer, except where these names show up in e.g., a listing of the contents of a library.

Some additional remarks with respect to function overloading:

- Do not use function overloading for functions doing conceptually different tasks. In the example above, the functions show are still somewhat related (they print information to the screen).

- However, it is also quite possible to define two functions `lookup`, one of which would find a name in a list while the other would determine the video mode. In this case the behavior of those two functions have nothing in common. It would therefore be more practical to use names which suggest their actions; say, `findname` and `videoMode`.

- **C++** does not allow identically named functions to differ only in their return values, as it is always the programmer’s choice to either use or ignore a function’s return value. E.g., the fragment

    ```
    printf("Hello World!\n");
    ```

    provides no information about the return value of the function `printf`. Two functions `printf` which only differ in their return types would therefore not be distinguishable to the compiler.

- In chapter 7 the notion of `const` member functions is introduced (cf. section 7.6). Here it is merely mentioned that classes normally have so-called member functions associated with them (see, e.g., chapter 5 for an informal introduction to the concept). Apart from overloading member functions using different parameter lists, it is then also possible to overload member functions by their `const` attributes. In other cases, these may have pairs of identically named member functions, having identical parameter lists. Then, these functions are overloaded by their `const` attribute. In such cases only one of these functions must have the `const` attribute.

### 2.5.5 Default function arguments

In C++ it is possible to provide ‘default arguments’ when defining a function. These arguments are supplied by the compiler when they are not specified by the programmer. For example:

```
#include <stdio.h>

void showstring(char *str = "Hello World!\n");

int main()
{
    showstring("Here’s an explicit argument.\n");

    showstring();             // in fact this says:
                              // showstring("Hello World!\n");
}
```

The possibility to omit arguments in situations where default arguments are defined is just a nice touch: it is the compiler who supplies the lacking argument unless it is explicitly specified at the call. The code of the program will neither be shorter nor more efficient when default arguments are used.

Functions may be defined with more than one default argument:

```cpp
void two_ints(int a = 1, int b = 4);

int main()
{
    two_ints();          // arguments:  1, 4
    two_ints(20);        // arguments: 20, 4
    two_ints(20, 5);     // arguments: 20, 5
}
```

When the function `two_ints` is called, the compiler supplies one or two arguments whenever necessary. A statement like `two_ints(,6)` is, however, not allowed: when arguments are omitted they must be on the right-hand side.

Default arguments must be known at compile-time since at that moment arguments are supplied to functions. Therefore, the default arguments must be mentioned at the function’s *declaration*, rather than at its *implementation*:

```cpp
// sample header file
extern void two_ints(int a = 1, int b = 4);

// code of function in, say, two.cc
void two_ints(int a, int b)
{
    ...
}
```

It is an error to supply default arguments in function definitions. When the function is used by other sources the compiler reads the header file rather than the function definition. Consequently the compiler has no way to determine the values of default function arguments. Current compilers generate compile-time errors when detecting default arguments in function definitions.

### 2.5.6 NULL-pointers vs. 0-pointers and nullptr (C++11)

In *C++* all zero values are coded as 0. In *C* NULL is often used in the context of pointers. This difference is purely stylistic, though one that is widely adopted. In *C++* NULL should be avoided (as it is a macro, and macros can—and therefore should—easily be avoided in *C++*, see also section 8.1.4). Instead 0 can almost always be used.

Almost always, but not always. As *C++* allows function overloading (cf. section 2.5.4) the programmer might be confronted with an unexpected function selection in the situation shown in section 2.5.4:

```cpp
#include <stdio.h>

void show(int val)
{
    printf("Integer: %d\n", val);
}

void show(double val)
{
    printf("Double: %lf\n", val);
}

void show(char const *val)
{
    printf("String: %s\n", val);
}

int main()
{
        show(12);
        show(3.1415);
        show("Hello World!\n");
}
```

In this situation a programmer intending to call `show(char const *)` might call `show(0)`. But this doesn’t work, as 0 is interpreted as `int` and so `show(int)` is called. But calling `show(NULL)` doesn’t work either, as C++ usually defines NULL as 0, rather than `((void *)0)`. So, `show(int)` is called once again. To solve these kinds of problems the new C++ standard introduces the keyword `nullptr` representing the 0 pointer. In the current example the programmer should call `show(nullptr)` to avoid the selection of the wrong function. The `nullptr` value can also be used to initialize pointer variables. E.g.,

```cpp
int *ip = nullptr;       // OK
int value = nullptr;     // error: value is no pointer
```

### 2.5.7 The ‘void’ parameter list

In C, a function prototype with an empty parameter list, such as

```c
void func();
```

means that the argument list of the declared function is not prototyped: the compiler does not warn against calling `func` with any set of arguments. In C the keyword `void` is used when it is the explicit intent to declare a function with no arguments at all, as in:

```c
void func(void);
```

As C++ enforces strict type checking, in C++ an empty parameter list indicates the total absence of parameters. The keyword `void` is thus omitted.

### 2.5.8 The ‘#define __cplusplus’

Each C++ compiler which conforms to the ANSI/ISO standard defines the symbol `__cplusplus`: it is as if each source file were prefixed with the preprocessor directive `#define __cplusplus`.

We shall see examples of the usage of this symbol in the following sections.

### 2.5.9 Using standard C functions

Normal C functions, e.g., which are compiled and collected in a run-time library, can also be used in C++ programs. Such functions, however, must be declared as C functions.

As an example, the following code fragment declares a function `xmalloc` as a C function:

```c
extern "C" void *xmalloc(int size);
```
