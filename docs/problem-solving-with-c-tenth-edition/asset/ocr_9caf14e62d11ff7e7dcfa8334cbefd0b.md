The exit statement shown earlier has nothing to do with classes and has nothing directly to do with streams, but it is often used in this context. The exit statement causes your program to end immediately. The exit function returns its argument to the operating system. To use the exit statement, your program must contain the following include directive:

```
#include <cstdlib>
```

When using exit, your program must also contain the following, normally either at the start of the file or at the start of the function body that uses exit:

```
using namespace std;
```

The function exit is a predefined function that takes a single integer argument. By convention, 1 is used as the argument if the call to exit was due to an error, and 0 is used otherwise.¹ For our purposes, it makes no difference what integer you use, but it pays to follow this convention since it is important in more advanced programming.

# The exit Statement

The exit statement is written

```
exit(Integer_Value);
```

When the exit statement is executed, the program ends immediately. Any Integer_Value may be used, but by convention, 1 is used for a call to exit that is caused by an error, and 0 is used in other cases. The exit statement is a call to the function exit, which is in the library with header file named cstdlib. Therefore, any program that uses the exit statement must contain the following directives:

```
#include <cstdlib>
using namespace std;
```

(These directives need not be given one immediately after the other. They are placed in the same locations as similar directives we have seen.)

> ¹ UNIX and Windows use 1 for error and 0 for success, but other operating systems may reverse this convention. You should ask your instructor what values to use.