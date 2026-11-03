a = 19, b = 3
Program completed

Here the expression FLAG == 1 is true, hence the statements corresponding to this #elif are compiled.

# 12.11.3 defined Operator

Syntax: defined(macro_name )

This operator is used only with #if and #elif directives. It evaluates to 1 if the macro_name has been defined using #define, otherwise it evaluates to zero. For example:

```
```c
#if defined(FLAG)
```
```

If the macro FLAG has been defined using #define, then the value of expression defined(FLAG) would be 1, otherwise its value would be 0.

# 12.11.4 #ifdef and #ifndef

The directives #ifdef and #ifndef provide an alternative short form for combining #if with defined operator.

#if defined(macro_name ) is equivalent to #ifdef macro_name

#if !defined(macro_name ) is equivalent to #ifndef macro_name

Syntax of #ifdef-

```
```c
#ifdef macro_name
......
#endif
```
```

If the macro_name has been defined with the #define directive, then the statements between #ifdef and #endif will be compiled. If the macro_name has not been defined or was undefined using #undef then these statements are not compiled.

Syntax of #ifndef-

Let us take a program-

```
```c
/*P12.17 Program to understand the use of #ifdef directive*/
#include<stdio.h>
#define FLAG
main()
{
 int a=20,b=4;
 #ifdef FLAG
 printf("FLAG is defined\n ");
 a++;
 b++;
 #endif
 printf("a = %d, b= %d\n",a,b);
 printf("Program completed\n");
}
```
```