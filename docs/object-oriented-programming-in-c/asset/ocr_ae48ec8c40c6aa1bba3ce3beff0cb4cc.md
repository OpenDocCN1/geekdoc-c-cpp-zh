# Namespace

Namespace is a new concept introduced by the ANSI C++ standards committee. This defines a scope for the identifiers that are used in a program. For using the identifiers defined in the namespace scope we must include the using directive, like

```
using namespace std;
```

Here, std is the namespace where ANSI C++ standard class libraries are defined. All ANSI C++ programs must include this directive. This will bring all the identifiers defined in std to the current global scope. using and namespace are the new keywords of C++. Namespaces are discussed in detail in Chapter 16.

# Return Type of main()

In C++, main() returns an integer type value to the operating system. Therefore, every main() in C++ should end with a return(0) statement; otherwise a warning or an error might occur. Since main() returns an integer type value, return type for main() is explicitly specified as int. Note that the default return type for all functions in C++ is int. The following main without type and return will run with a warning:

```
main()
{
      ......
      ......
}
```

# 2.4 More C++ Statements

Let us consider a slightly more complex C++ program. Assume that we would like to read two numbers from the keyboard and display their average on the screen. C++ statements to accomplish this is shown in Program 2.2.

![](bbox=[0.065, 0.695, 0.31, 0.72])

```
#include <iostream>

using namespace std;

int main()
{
    float number1, number2,
          sum, average;
```

(Contd)