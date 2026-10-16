
example, NULL might be 0 or 0L. In C, NULL is typically (void_*)0, which makes it illegal in C++ (§7.2.1):

```
int *p = NULL; // error :can't assign a void* to an int*
```

Using nullptr makes code more readable than alternatives and avoids potential confusion when a function is overloaded to accept either a pointer or an integer (§12.3.1).

## 7.3 Arrays

For a type T, T[size] is the type “array of size elements of type T.” The elements are indexed from 0 to size-1. For example:

```
float v[3]; // an array of three floats: v[0], v[1], v[2]
```

```
char*a[32]; // an array of 32 pointers to char: a[0] .. a[31]
```

You can access an array using the subscript operator, [], or through a pointer (using operator * or operator []; §7.4). For example:

```
void f()
{
int aa[10];
aa[6] = 9; // assign to aa's 7th element
int x = aa[99]; // undefined behavior
}
```

Access out of the range of an array is undefined and usually disastrous. In particular, run-time range checking is neither guaranteed nor common.

The number of elements of the array, the array bound, must be a constant expression (§10.4). If you need variable bounds, use a vector (§4.4.1, §31.4). For example:

```
void f(int n)
{
int v1[n]; // error : array size not a constant expression
vector<int> v2(n); // OK: vector with n int elements
}
```

Multidimensional arrays are represented as arrays of arrays (§7.4.2).

An array is C++’s fundamental way of representing a sequence of objects in memory. If what you want is a simple fixed-length sequence of objects of a given type in memory, an array is the ideal solution. For every other need, an array has serious problems.

An array can be allocated statically, on the stack, and on the free store (§6.4.2). For example:

```
int a1[10]; // 10 ints in static storage
```

```
void f() {
int a2 [20]; // 20 ints on the stack
int*p = new int[40]; // 40 ints on the free store
// ...
}
```

The C++ built-in array is an inherently low-level facility that should primarily be used inside the implementation of higher-level, better-behaved, data structures, such as the standard-library vector or array. There is no array assignment, and the name of an array implicitly converts to a pointer to its first element at the slightest provocation (§7.4). In particular, avoid arrays in interfaces (e.g., as function arguments; §7.4.3, §12.2.2) because the implicit conversion to pointer is the root cause of many common errors in C code and C-style C++ code. If you allocate an array on the free store, be sure to delete[] its pointer once only and only after its last use (§11.2.2). That’s most easily and most reliably done by having the lifetime of the free-store array controlled by a resource handle (e.g., string (§19.3, §36.3), vector (§13.6, §34.2), or unique_ptr (§34.3.1)). If you allocate an array statically or on the stack, be sure never to delete[] it. Obviously, C programmers cannot follow these pieces of advice because C lacks the ability to encapsulate arrays, but that doesn’t make the advice bad in the context of C++.

One of the most widely used kinds of arrays is a zero-terminated array of char. That’s the way C stores strings, so a zero-terminated array of char is often called a C-style string. C++ string literals follow that convention (§7.3.2), and some standard-library functions (e.g., strcpy() and strcmp(); §43.4) rely on it. Often, a char* or a const char* is assumed to point to a zero-terminated sequence of characters.

### 7.3.1 Array Initializers

An array can be initialized by a list of values. For example:

```
int v1[] = { 1, 2, 3, 4 };
char v2[] = { ‘a’, ‘b’, ‘c’, 0 };
```

When an array is declared without a specific size, but with an initializer list, the size is calculated by counting the elements of the initializer list. Consequently, v1 and v2 are of type int[4] and char[4], respectively. If a size is explicitly specified, it is an error to give surplus elements in an initializer list. For example:

```
char v3[2] = { ‘a’, ‘b’, 0 }; // error : too many initializers
char v4[3] = { ‘a’, ‘b’, 0 }; // OK
```

If the initializer supplies too few elements for an array, 0 is used for the rest. For example:

```
int v5[8] = { 1, 2, 3, 4 };
```

is equivalent to

```
int v5[] = { 1, 2, 3, 4 , 0, 0, 0, 0 };
```

There is no built-in copy operation for arrays. You cannot initialize one array with another (not even of exactly the same type), and there is no array assignment:

```
int v6[8] = v5; // error :can't copy an array(cannot assign an int* to an array)
v6 = v5; // error : no array assignment
```

Similarly, you can’t pass arrays by value. See also §7.4.
When you need assignment to a collection of objects, use a vector (§4.4.1, §13.6, §34.2), an array (§8.2.4), or a valarray (§40.5) instead.
An array of characters can be conveniently initialized by a string literal (§7.3.2).

### 7.3.2 String Literals

A string literal is a character sequence enclosed within double quotes:

```
“this is a string”
```

A string literal contains one more character than it appears to have; it is terminated by the null character, ‘\0’, with the value 0. For example:

```
sizeof("Bohr")==5
```

The type of a string literal is “array of the appropriate number of const characters,” so “Bohr” is of

type const char[5].

In C and in older C++ code, you could assign a string literal to a nonconst char*:

```
void f()
{
char*p = “Plato”; // error,but accepted in pre-C++11-standard code
p[4] = ‘e’; // error :assignment to const
}
```

It would obviously be unsafe to accept that assignment. It was (and is) a source of subtle errors, so please don’t grumble too much if some old code fails to compile for this reason. Having string literals immutable is not only obvious but also allows implementations to do significant optimizations in the way string literals are stored and accessed.

If we want a string that we are guaranteed to be able to modify, we must place the characters in a nonconst array:

```
void f()
{
char p[] = “Zeno”; // p is an array of 5 char
p[0] = ‘R’; // OK
}
```

A string literal is statically allocated so that it is safe to return one from a function. For example:

```
const char * error_message(int i)
{
// ...
return “range error”;
}
```

The memory holding “range error” will not go away after a call of error_message(). Whether two identical string literals are allocated as one array or as two is implementation defined (§6.1). For example:

```
const char* p = “Heraclitus”;
const char* q = “Heraclitus”;
```

```
void g() {
if (p == q) cout << “one!\n”; // the result is implementation-defined
// ...
}
```

Note that == compares addresses (pointer values) when applied to pointers, and not the values pointed to.

The empty string is written as a pair of adjacent double quotes, “”, and has the type const char[1]. The one character of the empty string is the terminating ‘\0’.
The backslash convention for representing nongraphic characters (§6.2.3.2) can also be used within a string. This makes it possible to represent the double quote (“) and the escape character backslash (\ ) within a string. The most common such character by far is the newline character, ‘\n’. For example:

```
cout<<“beep at end of message\a\n”;
```

The escape character, ‘\a’, is the ASCII character BEL (also known as alert), which causes a sound to be emitted.

It is not possible to have a “real” newline in a (nonraw) string literal:

```
“this is not a string
but a syntax error”
```

Long strings can be broken by whitespace to make the program text neater. For example:

```
char alpha[] = “abcdefghijklmnopqrstuvwxyz”
“ABCDEFGHIJKLMNOPQRSTUVWXYZ”;
```

The compiler will concatenate adjacent strings, so alpha could equivalently have been initialized by the single string

```
“abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ”;
```

It is possible to have the null character in a string, but most programs will not suspect that there are characters after it. For example, the string “Jens\000Munk” will be treated as “Jens” by standard library functions such as strcpy() and strlen(); see §43.4.

#### 7.3.2.1 Raw Character Strings

To represent a backslash ( \ ) or a double quote (“) in a string literal, we have to precede it with a backslash. That’s logical and in most cases quite simple. However, if we need a lot of backslashes and a lot of quotes in string literals, this simple technique becomes unmanageable. In particular, in regular expressions a backslash is used both as an escape character and to introduce characters representing character classes (§37.1.1). This is a convention shared by many programming languages, so we can’t just change it. Therefore, when you write regular expressions for use with the standard regex library (Chapter 37), the fact that a backslash is an escape character becomes a notable source of errors.
Consider how to write the pattern representing two words separated by a backslash (\):

```
string s = “\w\w”; // I hope I got that right
```

To prevent the frustration and errors caused by this clash of conventions, C++ provides raw string literals. A raw string literal is a string literal where a backslash is just a backslash (and a double quote is just a double quote) so that our example becomes:

```
string s = R“(w\w)”; // I’m pretty sure I got that right
```
