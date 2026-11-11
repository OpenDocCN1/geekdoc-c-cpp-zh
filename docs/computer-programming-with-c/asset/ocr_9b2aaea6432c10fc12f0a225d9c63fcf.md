![](bbox=[0.148, 0.125, 0.831, 0.383])

**Figure 2.45:** Execution of `cin>>a>>b;`

![](bbox=[0.243, 0.431, 0.733, 0.567])

**Figure 2.46:** Execution of `c = a + b;`

The last statement,

```
cout<<"The result of addition is: "<<c;
```

cascades the insertion operator so as to print the following message on the computer screen:

> The result of addition is: 300

> **NOTES**
> 
> The given program to perform addition of two numbers works only with C++ compilers and not with C compilers. This is because it uses `cout/cin` objects which are only supported by C++ and not by C. The program given below uses `printf()` and `scanf()` statements and hence works with both C as well as C++ compilers. It is acknowledged that `printf()` and `scanf()` statements are much complex to write compared to `cout/cin` statements, but if we want our program to work with both C and C++ we have no choice but to use them.

```
#include<stdio.h>

void main()
```