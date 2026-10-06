# Introduction to C Language, Variables, Data Types and Operators 37

When the above code is compiled and executed, it produces the following result:
value of area : 50

# The const Keyword

You can use const prefix to declare constants with a specific type as follows:
const type variable = value;
nThe following example explains it in detail.

```
#include<stdio.h>
int main(){
const LENGTH =10;
const WIDTH =5;
constchar NEWLINE = "\n";
int area;
a=LENGTH * WIDTH;
printf("value of area : %%d", area);
printf("%%c", NEWLINE);

return0;
}
```

When the above code is compiled and executed, it produces the following result:
value of area : 50

# VARIABLES

In programming, a variable is a container (storage area) to hold data.
To indicate the storage area, each variable should be given a unique name (identifier). Variable names are just the symbolic representation of a memory location.

For example:

+   1. int marks=95;

Here, marks is a variable of int type. Here, the variable is assigned an integer value 95.