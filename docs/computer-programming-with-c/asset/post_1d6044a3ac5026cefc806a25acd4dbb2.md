
![](img/57c0d966bb33c67a5a188e6bf39e4e02_135_0.png)

**Figure 4.8: Flow of execution**

![](img/57c0d966bb33c67a5a188e6bf39e4e02_136_0.png)

**Outer if block to test the condition C1**

Condition C2 will be tested only if C1 is true

**Inner if-else blocks to test the condition C2**

**Outer else block**

Condition C3 will be tested only if C1 is false

**Inner if-else blocks to test the condition C3**

```c
if (C1)
{
    if (C2)
    {
        /*Conditions C1 and C2 are true*/
    }
    else
    {
        /*Condition C1 is true
          whereas C2 is false*/
    }
}
else
{
    if (C3)
    {
        /*Condition C1 is false
          whereas C3 is true*/
    }
    else
    {
        /*Conditions C1 and C3 are false*/
    }
}
```

**Figure 4.9: Nesting of if-else**

![](img/57c0d966bb33c67a5a188e6bf39e4e02_136_1.png)

**Outer if block to test the condition a>b**

The condition a>c will be tested only if the condition a>b is true

**Outer else block**

The condition b>c will be tested only if the condition a>b is false

The conditions a>b and a>c are true. Hence, the value of variable a is maximum.

Condition a>b is true whereas, the condition a>c is false. Hence, the value of variable c is maximum.

Condition a>b is false whereas, the condition b>c is true. Hence, the value of variable b is maximum.

The conditions a>b and b>c are false. Hence, the value of variable c is maximum.

```c
if (a>b)
{
    if (a>c)
    {
        printf("The maximum is %d\n",a);
    }
    else
    {
        printf("The maximum is %d\n",c);
    }
}
else
{
    if (b>c)
    {
        printf("The maximum is %d\n",b);
    }
    else
    {
        printf("The maximum is %d\n",c);
    }
}
```

**Figure 4.10: Nesting of if-else to find the greatest of the three numbers**

```c
#include<stdio.h>
void main()
{
    int a,b,c;
    printf("Enter three numbers\n");
    scanf("%d %d %d",&a,&b,&c);
    if(a>b)
    {
        if(a>c)
        {
            printf("The maximum is %d\n",a);
        }
        else
        {
            printf("The maximum is %d\n",c);
        }
    }
    else
    {
        if(b>c)
        {
            printf("The maximum is %d\n",b);
        }
        else
        {
            printf("The maximum is %d\n",c);
        }
    }
}
```

**Output**

```
Enter three numbers
10 20 30
The maximum is 30
```

> **Can I write the condition in the program as:**
> **a>b>c**
> **so as to compare the value of variable a with b as well as c?**
>
> ---
>
> **a>b>c** is a **wrong** way to write the condition. This is because, the associativity of the relational operators is from left to right. Hence, the condition **a>b** will be evaluated first, which will return a value as **true(1)** or **false (0)**. Hence, the expression, **a>b>c** will compare the result of condition a>b with the value of variable c. This means that, the above expression will compare the value 0 or 1 with the value of variable c, thereby generating incorrect results. Therefore, we must write two different conditions as a>b and a>c so as to individually compare the value of variable a with b and c respectively. Hence, we have used nesting of if-else statements in the given program. This is because, we need to check two different conditions such that, the first condition compares the value of variable a with the value of variable b and the second condition compares the value of variable a with the value of variable c.

## 4.3 Logical Operators

The logical operators are used to connect multiple conditions so as to form a single expression. C/C++ supports three logical operators as listed below:

| Operator | Meaning |
| --- | --- |
| `&&` | Logical AND operation |
| \|\| | Logical OR operation |
| `!` | Logical NOT operation |

### 4.3.1 Logical AND operation

Given below is the sample expression that connects conditions C1 to CN using a logical AND operation.

```c
C1 && C2 && C3 && C4........ &&CN
```

The complete expression will be evaluated as true if each of the conditions C1, C2, C3 ... CN are individually evaluated as true. Note that, the whole expression will be evaluated as false if at least one condition from C1 to CN is evaluated as false.

As an example, if we consider the if block given in Figure 4.11, we combine two different conditions a>b and a>c using a logical AND operation. This means that, the control of execution will enter into the if block if and only if both the conditions a>b and a>c are true.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_138_0.png)

**Figure 4.11:** if block using && in the condition

### 4.3.2 Logical OR operation

Given below is the sample expression that connects conditions C1 to CN using a logical OR operation.

```c
C1 || C2 || C3 || C4........ || CN
```

The complete expression will be evaluated as true if at least one of the conditions C1 to CN is evaluated as true. Note that, the whole expression will be evaluated as false if none of the conditions from C1 to CN is true.

As an example, if we consider the if block given in Figure 4.12, we combine two different conditions y==15 and y==20 using a logical OR operation. This means that, the control of execution will enter into the if block if the value of variable y is either 15 or 20.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_139_0.png)

### 4.3.3 Logical NOT operation

Unlike the logical AND/logical OR which are binary operators, the logical NOT is a **unary** operator which works only with a single operand. We recollect that, any expression whose result is zero is considered as false whereas the expression whose result is nonzero is considered as true in C/C++. The logical NOT operator (`!`) is used to complement the result of the given condition. This means that, if the condition C1 is true then the condition !C1 will be evaluated as false, and if the condition C1 is false then the condition !C1 will be evaluated as true.

As an example, the code given in Figure 4.13 puts a condition as !p in the round parenthesis of the if block. The condition will be evaluated as true, because the value of variable p is initialized to zero. As the value of ‘p’ represents false, the value of !p will represent a true and hence the control of execution will enter the if block thereby printing the message Inside the if block on the computer screen.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_139_1.png)

## 4.4 else-if Ladder

Nesting of `if-else` blocks can sometimes increase the lines of code thereby making the program difficult to develop and maintain. `else-if ladder` can be used as an alternative to the nesting of multiple `if-else` blocks in the program thereby making the code more readable and easy to maintain when compared to ‘nesting’ of `if-else` statements.

Figure 4.14 gives the syntax of using else-if ladder in the program. The ladder consists of a single if block, multiple else-if blocks and a single else block as shown in Figure 4.14. The ladder evaluates conditions from top to bottom and as soon as the first condition from top is found to be true the control is transferred in the respective block of the else-if ladder and the rest of the ladder is skipped. The else block of the ladder will be executed only if all the conditions which are mentioned above in the ladder are evaluated as false.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_140_0.png)

**Figure 4.14:** Syntax of the else-if ladder

Given below is the full source to find the greatest of three numbers a, b and c using the else-if ladder and the logical operators:

```c
#include<stdio.h>
void main()
{
    int a,b,c;
    printf("Enter three numbers\n");
    scanf("%d %d %d",&a,&b,&c);
    if(a>=b && a>=c)
    {
        printf("The maximum is %d\n",a);
    }
    else if(b>=a && b>=c)
    {
        printf("The maximum is %d\n",b);
    }
    else
    {
        printf("The maximum is %d\n",c);
    }
}
```

**Output**

```
Enter three numbers
10 20 30
The maximum is 30
```

The code consists of three decision making blocks like the if block, else-if block and the else block. The if block will be executed if the condition,

`a>=b && a>=c`

is evaluated as true. Note that, the above expression will be evaluated as true, if value of the variable a is greater than (or equal to) b as well as c. Hence, the if block prints the value of the variable a as the maximum value as seen from the code. The latter part of the ladder will be skipped after the execution of the if block completes as shown in Figure 4.15.

However, if the condition specified in the if block is evaluated as false then the next condition specified as a part of the else if block will be evaluated. When the condition specified in the if block is evaluated as false, it indicates that the value of variable a is not the greatest value and hence the else if block determines if the value of variable b is the greatest using the following condition:

`b>=a && b>=c`
