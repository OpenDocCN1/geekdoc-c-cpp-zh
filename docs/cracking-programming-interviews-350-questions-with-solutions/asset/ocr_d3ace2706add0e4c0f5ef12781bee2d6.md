# Solution of Question 13

The output is

```
```text
ai: 6295552
size of array:20
enum a3 is: 30
length of array arr is :40
```
```

Please note that:

+   - Value of the second integer a1 is initialized with its own value which is indeterminate.
+   - The first template argument's default value type is looked up to find the typedef int and in the case of the second one, look up finds the template parameter.

# **Question 14** class scope variables

What is the output of this program?

Program 8.17: class scope variables

```
```cpp
#include <cstddef>
#include <iostream>

typedef int c;

enum { e = 10 };

struct A
{
    char arr[e];

    std::size_t fun()
    {
        return sizeof(c);
    }

    char c;

    enum { e = 20 };
};

int main()
{
    A a;
    std::cout << "size_of_arr is :"
              << sizeof(a.arr)/sizeof(char)
              << std::endl;
}
```
```