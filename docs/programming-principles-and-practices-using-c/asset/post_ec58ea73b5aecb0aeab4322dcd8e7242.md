
References are most common as function parameters, where they are used to avoid copying:

```cpp
void f(const string& s);
// ...
f("this string could be somewhat costly to copy, so we use a reference");
```

See §8.5.4–6.

## A.9 Functions

A *function* is a named piece of code taking a (possibly empty) set of arguments and optionally returning a value. A function is declared by giving the return type followed by its name followed by the parameter list:

```cpp
char f(string, int);
```

So, **f** is a function taking a **string** and an **int** returning a **char**. If the function is just being declared, the declaration is terminated by a semicolon. If the function is being defined, the argument declaration is followed by the function body:

```cpp
char f(string s, int i) { return s[i]; }
```

The function body must be a block (§8.2) or a **try**-block (§5.6.3).

A function declared to return a value must return a value (using the **return**-statement):

```cpp
char f(string s, int i) { char c = s[i]; }  // error: no value returned
```

The **main**() function is the odd exception to that rule (§A.1.2). Except for **main**(), if you don’t want to return a value, declare the function **void**; that is, use **void** as the “return type”:

```cpp
void increment(int& x) { ++x; }     // OK: no return value required
```

A function is called using the call operator (application operator), ( ), with an acceptable list of arguments:

```cpp
char x1 = f(1,2);                // error: f()’s first argument must be a string
string s = "Battle of Hastings";
char x2 = f(s);                  // error: f() requires two arguments
char x3 = f(s,2);                // OK
```

For more information about functions, see Chapter 8.

A function definition can be prefixed with **constexpr**. In that case, it must be simple enough for the compiler to evaluate when called with constant expression arguments. A **constexpr** function can be used in a constant expression (§8.5.9).

### A.9.1 Overload resolution

Overload resolution is the process of choosing a function to call based on a set of arguments. For example:

```cpp
void print(int);
void print(double);
void print(const std::string&);

print(123);      // use print(int)
print(1.23);     // use print(double)
print("123");    // use print(const string&)
```

It is the compiler's job to pick the right function according to the language rules. Unfortunately, in order to cope with complicated examples, the language rules are quite complicated. Here we present a simplified version.

Finding the right version to call from a set of overloaded functions is done by looking for a best match between the type of the argument expressions and the parameters (formal arguments) of the functions. To approximate our notions of what is reasonable, a series of criteria is tried in order:

- 1. Exact match, that is, match using no or only trivial conversions (for example, array name to pointer, function name to pointer to function, and **T to const T**)
- 2. Match using promotions, that is, integral promotions (**bool to int**, **char to int**, **short to int**, and their unsigned counterparts; see §A.8) and **float to double**
- 3. Match using standard conversions, for example, **int to double**, **double to int**, **double to long double**, **Derived* to Base*** (§14.3), **T* to void*** (§17.8), **int to unsigned int** (§25.5.3)
- 4. Match using user-defined conversions (§A.5.2.3)
- 5. Match using the ellipsis `...` in a function declaration (§A.9.3)

If two matches are found at the highest level where a match is found, the call is rejected as ambiguous. The resolution rules are this elaborate primarily to take into account the elaborate rules for built-in numeric types (§A.5.3).

For overload resolution based on multiple arguments, we first find the best match for each argument. If one function is at least as good a match as all other functions for every argument and is a better match than all other functions for one argument, that function is chosen; otherwise the call is ambiguous. For example:

```cpp
void f(int, const string&, double);
void f(int, const char*, int);

f(1,"hello",1);      // OK: call f(int, const char*, int)
f(1,string("hello"),1.0);     // OK: call f(int, const string&, double)
f(1,"hello",1.0);     // error: ambiguous
```

In the last call, the `"hello"` matches `const char*` without a conversion and `const string&` only with a conversion. On the other hand, `1.0` matches `double` without a conversion, but `int` only with a conversion, so neither f() is a better match than the other.

If these simplified rules don’t agree with what your compiler says and what you thought reasonable, please first consider if your code is more complicated than necessary. If so, simplify your code; if not, consult an expert-level reference.

### A.9.2 Default arguments

A general function sometimes needs more arguments than are needed for the most common cases. To handle that, a programmer may provide default arguments to be used if a caller of a function doesn’t specify an argument. For example:

```cpp
void f(int, int=0, int=0);
f(1,2,3);
f(1,2);      // calls f(1,2,0)
f(1);        // calls f(1,0,0)
```

Only trailing arguments can be defaulted and left out in a call. For example:

```cpp
void g(int, int =7, int);      // error: default for non-trailing argument
f(1,,1);                       // error: second argument missing
```

Overloading can be an alternative to using default arguments (and vice versa).

### A.9.3 Unspecified arguments

It is possible to specify a function without specifying the number or types of its arguments. This is indicated by an ellipsis ( . . . ), meaning “and possibly more arguments.” For example, here is the declaration of and some calls to what is arguably the most famous C function, `printf()` (§27.6.1, §B.11.2):

```cpp
void printf(const char* format ...);   // takes a format string and maybe more

int x = 'x';
printf("hello, world!");
printf("print a char '%c\n",x);      // print the int x as a char
printf("print a string \"%s\"",x);    // shoot yourself in the foot
```

The “format specifiers” in the format string, such as `%c` and `%s`, determine if and how further arguments are used. As demonstrated, this can lead to nasty type errors. In C++, unspecified arguments are best avoided.

### A.9.4 Linkage specifications

C++ code is often used in the same program as C code; that is, parts of a program are written in C++ (and compiled by a C++ compiler) and other parts in C (and compiled by a C compiler). To ease that, C++ offers *linkage specifications* for the programmer to say that a function obeys C linkage conventions. A C linkage specification can be placed in front of a function declaration:

```cpp
extern "C" void callable_from_C(int);
```

Alternatively it can apply to all declarations in a block:

```cpp
extern "C" {
    void callable_from_C(int);
    int and_this_one_also(double, int*);
    /* . . . */
}
```

For details of use, see §27.2.3.

C doesn’t offer function overloading, so you can put a C linkage specification on at most one version of a C++ overloaded function.

## A.10 User-defined types

There are two ways for a programmer to define a new (user-defined) type: as a class (*class*, *struct*, or *union*; see §A.12) and as an enumeration (*enum*; see §A.11).

### A.10.1 Operator overloading

A programmer can define the meaning of most operators to take operands of one or more user-defined types. It is not possible to change the standard meaning of an operator for built-in types or to introduce a new operator. The name of a user-defined operator (“overloaded operator”) is the operator prefixed by the keyword **operator**; for example, the name of a function defining **+** is **operator +**:

```cpp
Matrix operator+(const Matrix&, const Matrix&);
```

For examples, see **std::ostream** (Chapters 10–11), **std::vector** (Chapters 17–19, §B.4), **std::complex** (§B.9.3), and **Matrix** (Chapter 24).

All but the following operators can be user-defined:

```
?: . .* :: sizeof typeid alignas noexcept
```

Functions defining the following operators must be members of a class:

```
= [] () ->
```

All other operators can be defined as member functions or as freestanding functions. Note that every user-defined type has **=** (assignment and initialization), **&** (address of), and **,** (comma) defined by default.

Be restrained and conventional with operator overloading.

## A.11 Enumerations

An *enumeration* defines a type with a set of named values (*enumerators*):

```cpp
enum Color { green, yellow, red };          // "plain" enumeration
enum class Traffic_light { yellow, red, green }; // scoped enumeration
```

The enumerators of an **enum class** are in the scope of the enumeration, whereas the enumerators of a “plain” **enum** are exported to the scope of the **enum**. For example:

```cpp
Color col = red;              // OK
Traffic_light tl = red;       // error: cannot convert integer value
                              // (i.e., Color::red) to Traffic_light
```
