We have already seen how static can be used to declare variables and
functions that are not attached to a specific instance of the class, and now we have
sen how to use it to declare functions and variables with static linkage. There is
one more use of the static keyword that should be noted in passing. In C++, we
declare a local variable static. Such variables are initialized the first time the
function called called hold their value between function invocations. For example:

```
void nextPrime()
{
    static int n = 1;

    do {
        ++n;
    } while (!isPrime(n));

    return n;
}
```

Static local variables are similar to global variables, except that they are only
visible inside the function where they are defined.

# Namespaces

Namespaces are a mechanism for reducing the risks of name clashes in C++
programs. Name clashes are often an issue in large programs that use several
third-party libraries. In your own programs, you can choose whether you want to
namespaces.

Typically, we put a namespace around all the declarations in a header file to
ensure that the identifiers declared in that header file don't leak into the global
namespace. For example:

```
#ifndef SOFTWAREINC_RANDOM_H
#define SOFTWAREINC_RANDOM_H

namespace SoftwareInc
{
    extern int randomNumbers[128];

    void populateRandomArray();
}
```