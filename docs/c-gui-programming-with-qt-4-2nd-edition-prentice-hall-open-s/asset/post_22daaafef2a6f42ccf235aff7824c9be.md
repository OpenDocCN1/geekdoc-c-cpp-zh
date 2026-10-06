
and an assignment operator, and are normally instantiated on the stack with new. QDateTime, QImage, QString, and container classes such as QList<T>, QVector<T>, QMap<K, T>.

Other classes in the ("reference" type), QObject and its subclasses (QWidget, QTimer, QTcpSocket, etc.). These have virtual functions and cannot be copied. For example, QWidget represents a specific window or control on-screen. If there are 75 QWidget instances in memory, there are also 75 windows or controls on-screen. These classes are typically instantiated using the new operator.

## Global Variables and Functions

C++ lets us declare functions and variables that don't belong to any classes and are accessible from any other function. We have seen several examples of global functions, including main(), the program's entry point. Global variables are rarer, because they compromise modularity and thread reentrancy. It is still important to understand them because you might encounter them in code written by reformed programmers and other C++ users.

To illustrate how global functions and variables work, we will study a small program that prints a list of 128 pseudo-random numbers using a quick-and-dirty algorithm. The program's source code is spread over two .cpp files.

The first source file is random.cpp:

```cpp
int randomNumbers[128];

static int seed = 42;

static int nextNumber(){
  seed = 1009 + (seed * 2011);
  return seed;
}
void populateRandomArray(){
  for (int i = 0; i < 128; ++i)
    randomNumbers[i] = nextNumber();
}
```

The file declares two global variables (randomNumbers and seed) and two global functions (nextNumber() and populateRandomArray()). Two of the declarations contain the static keyword; these are visible only within the current compilation unit (random.cpp) and are said to have static linkage. The two others can be accessed from any compilation unit in the program; these have external linkage.

Static linkage is ideal for helper functions and internal variables that should not be used in other compilation units. It reduces the risks of having colliding identifiers (global variables with the same name or global functions with the same signature in different compilation units) and prevents malicious or otherwise ill-used users from accessing the internals of a compilation unit.

Let's now look at the second file, main.cpp, which uses the two global variables declared with external linkage in random.cpp:

```cpp
#include <iostream>

extern int randomNumbers[128];

void populateRandomArray();

int main() {
    populateRandomArray();
    for (int i = 0; i < 128; ++i)
        std::cout << randomNumbers[i] << std::endl;
    return 0;
}
```

We declare the external variables and functions before we call them. The external variable declaration (which makes an external variable in the current compilation unit) for randomNumbers starts with the extern keyword. Without extern, the compiler would think it has to deal with a variable definition, and the linker would complain because the same variable is defined in two compilation units (random.cpp and main.cpp). Variables can be declared as many times as we want, but be defined only once. The definition is what causes the compiler to reserve space for the variable.

The populateRandomArray() function is declared using a function prototype. The extern keyword is optional for functions.

Typically, we would put the external variable and function declarations in a header file and include it in all the files that need them:

```cpp
#ifndef RANDOM_H
#define RANDOM_H
extern int randomNumbers[128];

void populateRandomArray();
```

We have already seen how static can be used to declare variables and functions that are not attached to a specific instance of the class, and now we have seen how to use it to declare functions and variables with static linkage. There is one more use of the static keyword that should be noted in passing. In C++, we declare a local variable static. Such variables are initialized the first time the function is called and hold their value between function invocations. For example:

```cpp
void nextPrime()
{
    static int n = 1;

    do {
        ++n;
    } while (!isPrime(n));

    return n;
}
```

Static local variables are similar to global variables, except that they are only visible inside the function where they are defined.

## Namespaces

Namespaces are a mechanism for reducing the risks of name clashes in C++ programs. Name clashes are often an issue in large programs that use several third-party libraries. In your own programs, you can choose whether you want to use namespaces.

Typically, we put a namespace around all the declarations in a header file to ensure that the identifiers declared in that header file don't leak into the global namespace. For example:

```cpp
#ifndef SOFTWAREINC_RANDOM_H
#define SOFTWAREINC_RANDOM_H

namespace SoftwareInc
{
    extern int randomNumbers[128];

    void populateRandomArray();
}

#endif
```

(Notice that we have also renamed the preprocessor macro used to avoid multiple inclusions, reducing the risk of a name clash with a header file of the same name but located in a different directory.)

The de-namespace syntax is similar to that of a class, but it doesn't end with a semicolon. Here's the new random.cpp file:

```cpp
#include "random.h"
```

```cpp
int SoftwareInc::randomNumbers[128];
static int seed = 42;
static int nextRandomNumber() {
    seed = 1009 + (seed * 2011);
    return seed;
}
```

```cpp
void SoftwareInc::populateRandomArray() {
    for (int i = 0; i < 128; ++i)
        randomNumbers[i] = nextRandomNumber();
}
```

Unlike classes, namespaces can be "reopened" at any time. For example:

```cpp
namespace Alpha {
    void alpha1();
    void alpha2();
}
```

```cpp
namespace Beta {
    void beta1();
}
```

```cpp
namespace Alpha {
    void alpha3();
}
```

This makes it possible to define hundreds of classes, located in as many header files, as part of a single namespace. Using this trick, the Standard C++ library puts all its identifiers in std namespace. In Qt, namespaces are used for global-like identifiers such as Qt::AlignBottom Qt::yellow. For historical reasons, Qt classes do not belong to any namespace but are prefixed with the letter 'Q'.

To refer to an identifier declared in a namespace from outside the namespace, we prefix it with the name of the namespace (and ::). Alternatively, we can use one of the following three mechanisms, which are aimed at reducing the number of keystrokes we must type.

- **We can define a namespace alias**

```cpp
namespace ElPuebloDeReinaDeLosAngeles
{
    void beverHills();
    void culverCity();
    void malibu();
    void santaMonica();
}

namespace LA = ElPuebloDeReinaDeLosAngeles;
```

After the alias definition, the aliases can be used instead of the original name.

- **We can import a single identifier from a namespace:**

```cpp
int main()
{
    using ElPuebloDeReinaDeLosAngeles::beverHills;
    beverHills();
    ...
}
```

The using declaration allows us to access a given identifier from a namespace without having to prefix it with the name of the namespace.

- **We can import an entire namespace with a single directive:**

```cpp
int main()
{
    using namespace ElPuebloDeReinaDeLosAngeles;
    santaMonica();
    malibu();
    ...
}
```

With this approach, name clashes are more likely to occur. If the compiler complains about an ambiguous name (e.g., two classes with the same name defined in two namespaces), we can always qualify the identifier with the name of the namespace when referring to it.

## The C++ Preprocessor

The C++ preprocessor is a program that converts a .cpp source file containing # directives (such as #include, #ifdef, and #endif) into a source file that contains no directives. The preprocessor performs textual operations on the source file, such as conditional compilation, file inclusion, and macro expansion. Normally, the preprocessor is invoked automatically by the compiler, but most systems still offer a way to invoke it alone (often through a -E compiler option).

- #include the contents of the file specified within angle brackets (<>) or double quotes(""), depending on the header file is installed at a standard location or is part of the current project. The file name may contain ... and / (which Windows compilers correctly interpret as the directory separator). For example:
#include "../shared/globaldefs.h"
- #define defines a macro. Occurrences of the macro appearing after the #define directive are replaced with the macro's definition. For example, the directive
#define PI 3.14159265359

tells the preprocessor to replace all future occurrences of the token PI in the current compilation unit with the token 3.14159265359. To avoid clashes with variable and class names, it is common practice to give macros all-uppercase names. It is possible to define macros that take arguments:
#define SQUARE(x) ((x) * (x))

In the macro body, it is good style to surround all occurrences of the parameters with parentheses, as well as the entire body, to avoid problems with operator precedence. After all, we want 7 * SQUARE(2 + 3) to expand 7 ((2 + 3), (2 + 3)), not to 7 + 2 + 3 + 2 + 3.

C++ normally allows us to define macros on the command line, using

img/5a524abdf0b0d58fa99d30abb4463611_1063_0.png)
