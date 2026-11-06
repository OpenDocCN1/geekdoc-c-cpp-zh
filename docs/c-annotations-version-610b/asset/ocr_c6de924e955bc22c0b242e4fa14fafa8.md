So far, so good. All is well as long as we’re using but one object. What about allocating an array of objects? Initialization is performed as usual. But as with `delete`, `delete[]` cannot be called when the buffer was allocated statically. Instead, when multiple objects were initialized using placement `new` in combination with a statically allocated buffer all the objects’ destructors must be called explicitly, as in the following example:

```
```cpp
using std::string;

char buffer[3 * sizeof(string)];
string *sp = new(buffer) string [3];

for (size_t idx = 0; idx < 3; ++idx)
    sp[idx].~string();
```
```

# ## 9.2 The destructor

Comparable to the constructor, classes may define a *destructor*. This function is the constructor’s counterpart in the sense that it is invoked when an object ceases to exist. A destructor is usually called automatically, but that’s not always true. The destructors of dynamically allocated objects are not automatically activated, but in addition to that: when a program is interrupted by an `exit` call, only the destructors of already initialized global objects are called. In that situation destructors of objects defined *locally* by functions are also *not* called. This is one (good) reason for avoiding `exit` in C++ programs.

Destructors obey the following syntactical requirements:

+   - a destructor’s name is equal to its class name prefixed by a tilde;
+   - a destructor has no arguments;
+   - a destructor has no return value.

Destructors are declared in their class interfaces. Example:

```
```cpp
class Strings
{
    public:
        Strings();
        ~Strings();      // the destructor
};
```
```

By convention the constructors are declared first. The destructor is declared next, to be followed by other member functions.

A destructor’s main task is to ensure that memory allocated by an object is properly returned when the object ceases to exist. Consider the following interface of the class `Strings`:

```
```cpp
class Strings
{
    std::string *d_string;
    size_t d_size;

    public:
        Strings();
        Strings(char const *const *cStrings, size_t n);
        ~Strings();
```
```