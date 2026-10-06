# #pragma

The #pragma preprocessor directive is used to provide additional information to the compiler. The #pragma directive is used by the compiler to provide machine or operating-system feature. Different compilers can provide different usage of #pragma directive.

# Syntax:

```
#pragma token

Example:
#include<stdio.h>
#include<conio.h>

void func();
#pragma startup func
#pragma exit func
void main(){
printf("\nl am in main");
getch();
}

void func(){
printf("\nl am in func");
getch();
}

Output
Iam in func
Iam in main
Iam in func
```

# C Tokens

+   - C tokens are the basic buildings blocks in C language which are constructed together to write a C program.
- Each and every smallest individual units in a C program are known as C tokens.