If nothing else this is easier to read than the version using `const char*`. Use `string` as your preferred way of storing text.

Technically a `string` is not a basic data type in C++. This is why you have to have write `#include <string>`. By default, only the basic data types are available in C++ unless you have an `#include` statement to indicate that you want to use a more complex data type.

We will talk at length about complex data types in this book. In fact, to some extent this book is about creating your own sophisticated data types in C++. We will create data objects to represent things such as options and market data.

# ## 2.5 Operators

# ### 2.5.1 The `sizeof` operator

You can find the size (in bytes) of a data type using the `sizeof` operator. For example, the code

```
```cpp
size_t charSize = sizeof(char);
cout << "A char takes up ";
cout << charSize << " byte\n";
```
```

can be used to confirm that a `char` takes up one byte as claimed.

# ### 2.5.2 Mathematical operations

You can perform various operations on numbers. We have already discussed `+`, `*`, `-` and `/`.

One other mathematical operator that you probably wouldn't think of is `%`. This is called the modulus operator. It computes the remainder on division. So, for example, `13 % 5` is 3.

We have also already seen that you can't raise a number to a given power using the `^` operator. Instead you must use the function `pow`.

This function is defined in the library called `cmath`. The statement

```
```cpp
#include <cmath>
```
```

at the beginning of all our programs means "we want to be able to use the functions in the cmath" library.

There are plenty of other functions in the `cmath` library, such as `sin`, `cos`, and so forth. The syntax for calling a function in C is the same as in mathematics.

```
```cpp
double x = 2.345;
```
```