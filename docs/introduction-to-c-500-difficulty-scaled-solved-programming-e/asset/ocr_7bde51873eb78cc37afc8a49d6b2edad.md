# 11 • Functions 297

The linkage of a global variable or function is external by default, that is, it may be shared in different files. However, if it is declared as static, the linkage changes to internal, which means that it is visible only within the file in which is defined. For example:

```
#include <iostream>
using namespace std;

static void test(int i);
static int flag;

int main() {
  ...
}

static void test(int i) {
}
```

flag and test() are visible only within this file, which means that they cannot be accessed by functions in other files. In particular, flag has file scope, static storage duration, but internal linkage. The main reason of declaring them as static is from other files, preventing it from being used as extern when it is not desired. In a large program split in several files, typically written by different programmers, it is a good idea to declare your functions as static. Besides hiding information, another reason is if the code of a static function should be modified later, you won't worry if those changes affect functions in other files (with the exception that the pointer to function is passed to a function of another file). Also, you don't have to worry if the names you choose are used in other files as well, if it happens, there will be no conflict. Since the linkage is internal, the same names can be reused in other files. Another way to define names with internal linkage, and this is what is recommended, is by using unused namespaces, as we'll see in Chapter 25. However, since static is used quite extensively in existing code it is good to know how it is used.

Let's see one example that combines these concepts. Consider the following program which consists of two source files. Both must be compiled and linked to produce the final executable. Can you tell what it displays?

```
// First file.
#include <iostream> // Example 11.19

void test();
int ext = 10;
static int st = 20;

int main() {
  test();
  std::cout << ext << ' ' << st << '\n';
  return 0;
}
```

```
// Second file.
#include <iostream>

extern int ext;
static int st;
```