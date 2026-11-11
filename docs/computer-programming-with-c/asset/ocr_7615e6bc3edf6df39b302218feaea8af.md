Hence the statement,

```
printf("c=%d\n",*r);
```

will generate the following output:

```
c=42.9
```

Writing p in the code, will give the value stored inside the pointer p. We know that pointer p contains address of variable a, that is 1000. Hence, the result of this token will be 1000.

Hence the statement,

```
printf("Address of a is %u\n",p);
```

will generate the following output:

```
Address of a is 1000
```

Writing token r in the code, will give the address stored inside r  that is 3000. Hence the statement,

```
printf("Address of c is %u\n",r);
```

will generate the following output:

```
Address of c is 3000
```

# 8.4  Types of Function Calls

# 8.4.1  Call by value

Consider the given code which consists of two functions main() and f1(). The function f1() takes one integer type argument and increments the integer value passed to it. The function main() calls a function f1() by passing the value of its local variable a which is created in main().

Due to the function call, value of variable a in main() is passed to variable p which is the formal argument of f1(). Since value of the variable is passed from calling function to the called function, the mechanism is named as ‘call by value’.

```
#include<stdio.h>
void f1(int);
void main()
{
int a=10;
printf("Before call a=%d\n",a);
f1(a);
printf("After call a=%d\n",a);
}
void f1(int p)
{
p++;
}
```