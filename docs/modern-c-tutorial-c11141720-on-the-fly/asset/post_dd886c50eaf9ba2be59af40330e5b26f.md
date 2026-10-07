
## 1.2 Compatibilities with C

CHAPTER 01: TOWARDS MODERN C++

```cpp
}
#endif
```

```cpp
// foo.c
int add(int x, int y) {
    return x+y;
}
```

```cpp
// 1.1.cpp
#include "foo.h"
#include <iostream>
#include <functional>
```

```cpp
int main() {
    auto out = std::ref(std::cout << "Result from C code: " << add(1,2));
    out.get() << "\n";
    return 0;
}
```

You should first compile the C code with gcc

```
gcc -c foo.c
```

Compile and output the foo.o file, and link the C++ code to the .o file using clang++ (or both compile to .o and then link them together)

```cpp
clang++ 1.1.cpp -std=c++2a -o 1.1
```

Of course, you can use Makefile to compile the above code:

```makefile
C = gcc
CXX = clang++
SOURCE_C = foo.c
OBJECTS_C = foo.o
SOURCE_CXX = 1.1.cpp
TARGET = 1.1
LDFLAGS_COMMON = -std=c++2a
```

## Further Readings

all:

```makefile
$$(C) -c $(SOURCE_C)
$(CXX) $(SOURCE_CXX) $(OBJECTS_C) $(LDFLAGS_COMMON) -o $(TARGET)
```

clean:

```makefile
rm -rf *. $(TARGET)
```

Note: Indentation in Makefile is a tab instead of a space character. If you copy this code into your editor, the tab may be automatically replaced. Please ensure the indentation in the Makefile. It is done by tabs.

If you don't know the use of Makefile, it doesn't matter. In this tutorial, you won't build code that is too complicated. You can also read this book by simply using clang++-std=c++2a on the command line.

If you are new to modern C++, you probably still don't understand the following small piece of code, above:

```cpp
auto out = std::ref(std::cout << "Result from C code: " << add(1, 2));
out.get() << "\n";
```

Don't worry at the moment, we will come to meet them in our later chapters.

## Further Readings

- A Tour of C++ (2nd Edition) Bjarne Stroustrup
- History of C++
- C++ compiler support
- Incompatibilities Between ISO C and ISO C++

## Chapter 02: Language Usability Enhancements

When we declare, define a variable or constant, and control the flow of code, object-oriented functions, template programming, etc., before the runtime, it may happen when writing code or compiler compiling code. This we usually talk about language usability, which refers to the language behavior that occurred before the runtime.

## 2.1 Constants

### nullptr

The purpose of nullptr appears to replace NULL. In a sense, traditional C++ treats NULL and 0 as the same thing, depending on how the compiler defines NULL, and some compilers define NULL as ((void*)0). Some will define it directly as 0.

C++ does not allow to implicitly convert void * to other types. But if the compiler tries to define NULL as ((void*)0), then in the following code:

```cpp
char *ch = NULL;
```

C++ without the void * implicit conversion to define NULL as 0. This still creates a problem. Defining NULL to 0 will cause the overloading feature in C++ to be confusing. Consider the two following functions:

```cpp
void foo(char*);
void foo(int);
```

Then the foo(NULL) statement will call foo(int), which will cause the code to be counterintuitive.

To solve this problem, C++11 introduced the nullptr keyword, which is specifically used to distinguish null pointers. The type of nullptr is nullptr_t, which can be implicitly converted to any pointer or pointer type, and can be compared equally or unequally with them.

You can try to compile the following code using clang++:

```cpp
#include <iostream>
#include <type_traits>

void foo(char *);
void foo(int);

int main() {
    if (std::is_same<decltype(NULL), void(*)>::value) {
        std::cout << "NULL = 0" << std::endl;
    }
    if (std::is_same<decltype(NULL), void(*)>::value) {
        std::cout << "NULL = (void*)0" << std::endl;
    }
    if (std::is_same<decltype(NULL), nullptr_t>::value) {
        std::cout << "NULL = nullptr" << std::endl;
    }

    foo(0);              // will call foo(int)
    foo(NULL);      // doesn't compile
    foo(nullptr);      // will call foo(char*)
    return 0;
}

void foo(int i) {
    std::cout << "foo(int) is called" << std::endl;
}
```

The outputs are:

```
foo(int) is called
foo(char*) is called
```

From the output we see that NULL is different from 0 and nullptr. So, develop the habit of using nullptr directly. In addition, in the code, used decltype and std::is_same are modern C++ syntax. In simple terms, decltype is used for type derivation, and std::is_same is used to compare the equality of the two types. We will discuss this in detail in the constexpr section.

### constexpr

C++ itself already has the concept of constant expressions, such as 1+2, 3*4. Such expressions always produce the same result without side effects. If the compiler can directly optimize and embed these expressions into the program at compile time, it will increase the performance of the program. A very obvious example is in the definition of an array:

```cpp
#include <iostream>
#define LEN 10

int len_foo() {
    int i = 2;
    return i;
}

constexpr int len_foo() {
    return 5;
}

constexpr int fibonacci(int n) {
    return n == 1 || n == 2 ? 1 : fibonacci(n-1) + fibonacci(n-2);
}

int main() {
    char arr1[10]; // legal
    char arr2[LEN]; // legal
    int len = 10;
    // arr3[len];               // illegal

    const int len2 = len + 1;
    constexpr int len2c = len + 2 + 3;
    // arr4[len2];              // illegal, but ok for most compilers
    char arr4[len2c];         // legal

    // arr5[len_foo()];          // illegal
    char arr6[len_foo() = 2 ? 1];  // legal

    // 1, 2, 3, 5, 8, 13, 21, 34, 55
    std::cout << fibonacci(10) << std::endl;

    return 0;
}
```

In the example above, arr4[len2] may be confusing because len2 has been defined as a constant. Why is arr4[len2] illegal? This is because the length of the array in the C++ standard must be a constant expression, and for len2, this is a const constant, not a constant expression, even if this is supported by most compilers, but it is an illegal behavior, we need to use the constexpr feature introduced in C++11, which will be introduced next, to solve this problem; for arr5 before C++98 the compiler cannot know that len_foo() actually returns a constant at runtime, which causes illegal production.

Note that most compilers now have their own compiler optimizations. Many illegal behaviors become legal under the compiler's optimization. If you need to reproduce the error, you need to use the older version of the compiler.

C++11 provides to let the user explicitly declare the function or object constructor will become a constant expression at compile time. This keyword explicitly tells the compiler that it should verify that len_foo should be a compile time expression. Constant expression.

In addition, the function of constexpr can use recursion:

```cpp
constexpr int fibonacci(int n) {
    return n == 1 || n == 2 ? 1 : fibonacci(n-1) + fibonacci(n-2);
}
```

Starting with C++14, the constexpr function can use simple statements as local variables, loops, and branches internally. For example, the code cannot be compiled under the C++11 standard.

## 2.2 Variables and initialization

```cpp
constexpr int fibonacci(int n) {
    if(n == 1) return 1;
    if(n == 2) return 1;
    return fibonacci(n-1) + fibonacci(n-2);
}
```

To this, we can write a simplified version of this to make the function available from C++11:

```cpp
constexpr int fibonacci(int n) {
  return n == 1 || n == 2 ? 1 : fibonacci(n-1) + fibonacci(n-2);
}
```

### if-switch

In Traditional C++, the declaration of the variable can declare a temporary int even though it can be located anywhere, even for a statement, but there is no way to declare a temporary variable in the if and switch statements. E.g:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
```

```cpp
int main() {
  std::vector<int> vec = {1, 2, 3, 4};

  // since c++17, can be simplified by using `auto`
  const std::vector<int>::iterator itr = std::find(vec.begin(), vec.end(), 2);
  if (itr != vec.end()) {
    *itr = 3;
  }

  if (const std::vector<int>::iterator itr = std::find(vec.begin(), vec.end(), 3);
      itr != vec.end()) {
    *itr = 4;
  }

  // should output: 1, 4, 3, 4. can be simplified using `auto`
  for (std::vector<int>::iterator element = vec.begin(); element != vec.end(); ++element) {
    std::cout << *element << std::endl;
  }
}
```
