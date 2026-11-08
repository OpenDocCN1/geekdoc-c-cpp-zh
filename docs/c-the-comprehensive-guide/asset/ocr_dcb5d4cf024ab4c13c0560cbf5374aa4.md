exactly with Listing 23.29. If you want to cover other number ranges, you should take a closer look at the relatives char and short as well as long and long long in Section 4.4.

# ### The “bool” Type

While an int variable can assume many states, a bool variable is fixed to one of two states: true or false.

Comparisons are expressions whose result is of type bool, and you can store their result in a variable of this type instead of using it directly.

```
```cpp
// https://godbolt.org/z/zk9e9n48
#include <iostream>            // cout
int main(int argc, const char* argv[]) {
    bool withParameters = argc > 1;    // comparison result stored
    if (withParameters) {              // ... and used
        std::cout << "You have called the program with parameters.\n";
    }
    return 0;
}
```
```

Listing 4.16 Variables of type bool can store the result of a comparison.

# ### The Types “`const char*`” and “`std::string`”

These two very different types have the same purpose: their variables represent strings—that is, text strings, like texts, messages, notes, names, and so on. Depending on the task, sometimes the “pointer variant” `const char*`, which cannot deny its origin in C, is suitable, and sometimes the `std::string` “class” from the C++ standard library is suitable.

> > **Pointers, Addresses, and Memory Areas**
> >
> > Note the asterisk `*` in `char*` or `const char*`. This tells you: “I am only storing the address of something.” This means that there is a `char` where the variable points to. There is also `int*` as a pointer to an `int` and so on.
> >
> > When it comes to character strings, however, another piece of information is missing because the pointer only contains the address of the first character; others may follow. In C, it is common for a text to extend to the next `char` with the value `0`, also written `'\0'`, this is then a C string. The C function `printf(const char* fmt, ...)` works in this way, for example.
> >
> > Other functions prefer to take pointers and a length, such as `memcpy(void* dest, const void* src, size_t n)`. Here, starting from `src`, the next `n` bytes are copied to `dest`.
> >
> > The third variant, using pointers to define a range, is often used in C++ for containers and algorithms. For example, you can use `std::find(const char* beg, const char* end, char c)` to find the character `c` between `beg` and `end`.