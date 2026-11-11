![](bbox=[0.149, 0.109, 0.882, 0.504])

# 7.9.4  `extern` storage class

The variable which is defined in some other cpp file is called an external variable. We can access the value of such variables using the keyword `extern` as shown in Figure 7.37.

As seen from Figure 7.37, the variable `a` is declared as a global variable in the file `p1.cpp` with a value initialized as 10. The value of variable `a` can also be accessed in some other file say `p2.cpp` provided that the variable `a` is declared as extern in the file `p2.cpp`. The keyword informs the compiler that the variable `a` is actually declared in some file. Hence, we can now access the value of a variable which is defined in some other file using a keyword `extern`.

# 7.10  Inline Functions in C/C++

We understand that when a function is ‘called’ the control is transferred to the function definition. For example, let us consider a function `f1()` that prints a message Learning C and C++ on the computer screen as shown in the code below:

```
```cpp
#include<stdio.h>
void f1()
{
printf("Learning C and C++\\n");
}
```
```