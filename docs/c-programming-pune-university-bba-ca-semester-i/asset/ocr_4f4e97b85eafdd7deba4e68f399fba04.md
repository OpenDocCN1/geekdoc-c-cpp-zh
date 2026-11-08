# ### pre-increment (++ variable)

In pre-increment first increment the value of variable and then used inside the expression (initialize into another variable).

# #### Syntax

```
`++ variable;`
```

# #### *Example pre-increment*

```
```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int x,i;
    i=10;
    x=++i;
    printf("x: %d",x);
    printf("i: %d",i);
    getch();
}
```
```

# #### **Output:**

```
```
x: 11
i: 11
```
```

In above program first increase the value of i and then used value of i into expression.

# ### post-increment (variable ++)

In post-increment first value of variable is used in the expression (initialize into another variable) and then increment the value of variable.

# #### Syntax

```
`variable ++;`
```

# #### *Example post-increment*

```
```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int x,i;
    i=10;
    x=i++;
    printf("x: %d",x);
```
```