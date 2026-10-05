
# OPERATORS

# Examples

```
int a=10,b=20;
printf("%d", a+b); -> outputs 30
printf("%f", a+5.0); -> outputs 15.000000
printf("%d", a+'a'); -> outputs 107
printf("%d", a-(-10)); -> outputs 7
printf("%d",a+10-b); -> outputs 40
```

Note that, when we add a character constant with another numeric, the ASCII value of the character is added up. Hence the result '107' in the third example.

# Subtraction operator

This operator subtracts the second operand from the first. If the first operand is greater than the second, the operator returns a positive value; else, it gives a negative answer.

# Examples

```
int a=10,b=20;
printf("%d", a-b); -> outputs -10
printf("%f", a-5.0); -> outputs 5.000000
printf("%d", a-'a'); -> outputs 87
printf("%d", a-(-3)); -> outputs 13
printf("%d",a+10-b); -> outputs 0
```

# Multiplication operator

This operator gives the product of two numbers. Like addition and subtraction operators, it can operate on int, float and char operands.

# Examples

```
int a=10,b=20;
printf("%d", a*b); -> outputs 200
printf("%f", a*5.0); -> outputs 50.000000
printf("%d", a*'a'); -> outputs 970
printf("%d", a*(-3)); -> outputs -30
printf("%d",a*10-b); -> outputs 2000
```

# Division operator

This operator divides the first operand by second operand and gives the quotient as the value. Like traditional mathematics, the denominator should not be equal to zero.(The Divide By Zero exception!)

# Examples

```
int a=20,b=10;
printf("%d", a/b); -> outputs 2
printf("%f", 20/10.0); -> outputs 2.000000
printf("%d",19/'a'); -> outputs 2
printf("%f",10/20.0); -> outputs 0.500000
```

# Modulo operator

This operator returns the remainder after dividing the first operand by second.
The result will be positive if any of the operands is negative. There is one exception regarding the operands’ nature. This operator will not work with decimal numbers and exponential operands. They are considered to be invalid operands.

# Examples

```
int a=11, b=-3;
printf("%d",a%b) -> outputs 2
printf("%d",20%30) -> outputs 20
printf("%d", 33%20) -> outputs 13
```

# 4.2.2. Assignment operators

This operator is well known to the readers. They have used plenty of times so far. Weird? Well, you have seen a=11, b=-3, a=10, b=20 in the previous examples? We call these operations ‘Initialization’. We use assignment operator (=) for performing initialization.

These operators are not only used to perform initialization. But they can assign the result of an expression to another variable using ‘equality operator (=)’(Note that an expression is the combination of set of variables, for example, a+b-c*10 is an integer expression).

There are some of the shorthand assignment operators available in ‘C’. They are listed below.

- +=
- =
- *=
- /=
- %=

Looking at the examples would make the usage of the operators clearer.

# Examples

# Initialization examples.

```
int a=10,a=1;
float b=20.0;
char c='a';
char c1[1];
char c2[12]="programming";
a1=a; -> assigning 10 to a1.
Expression example.
(Using the above declarations)
b=50.0-30; -> assigns 30 to b!
Shorthand operators.
(Using the previous declarations)
a+=10; -> equivalent to a+10; -> outputs 20
b=-5; -> equivalent to b-5; -> outputs 15
c1*=35; -> equivalent to c1*=35; -> outputs # (When it is multiplied by 35, it is equal to 35 is the ASCII value for the symbol hash).
a/=2; -> equivalent to a/2; -> outputs 5
a%=2; -> equivalent to a%2; -> outputs 0
```

With this section, the user would have been familiar with arithmetic and assignment operators. In the next section, the reader will be introduced ‘Logical operators’!

# OPERATORS Logical operators

# 4.2.3.

These are special kinds of operators that work on the basis of 'Truth tables'. There are 3 operators in this section. They are,

- 1. && (Logical AND)
- 2. || (Logical OR)
- 3. !(Logical NOT)

AND operator and OR operator operate on two operands. Whereas, AND is not a unary operator who works on single operand. Look at the truth tables given below for understanding the logic behind these operators.

0 indicates FALSE condition, 1 indicates TRUE condition

| First operand | Second operand | First operand && Second operand |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |
| Table 4.1 AND truth table |

As it can be observed from the Table 4.1, only if both the operands are evaluated to true, the result will be TRUE. Else if any of the operands is FALSE, the answer will be FALSE.

Unlike AND operator, who expects both the operands to be evaluated to TRUE for the answer to be TRUE, OR operator needs at least one of the operands to be TRUE. Refer to the Table 4.2 for truth values.

0 indicates FALSE condition, 1 indicates TRUE condition

| First operand | Second operand | First operand || Second operand |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |
| Table 4.2 OR truth table |

NOT operator is a unary operator, which flips the value of operand. For example, if the operand is true, it outputs false. If the operand is false, it outputs true. Having seen the truth tables, it would be better if the concepts are explained through a program.

# 54 C-SIMPLER

```c
#include<stdio.h>
void main() {
    int a,b;
    int choice;
    printf("choose the logical operation to be performed!\n");
    printf("enter the first number..\n");
    scanf("%d",&a);
    printf("enter the second number..\n");
    scanf("%d",&b);
    do{
        switch (choice) {
            case 1:
                printf("%d && %d\n", a, b);
                break;
            case 2:
                printf("%d || %d\n", a, b);
                break;
            case 3:
                printf("!%d\n", a);
                break;
            case 4:
                printf("Exiting...\n");
                break;
        }
        printf("\nchoose the operation:\n");
        scanf("%d",&choice);
    } while (choice!=4);
}
```

# Program 4.1 Logical operators

```c
#include<stdio.h>
void main() {
    int a=10,b=20;
    printf("%d && %d\n", a, b);
    printf("%d || %d\n", a, b);
    printf("!%d\n", a);
}
```

# Program 4.2 Logical operators example

```c
#include<stdio.h>
void main() {
    char username[15],pwd[8];
    printf("Login Form\n");
    printf("Please Enter the Username:\n");
    gets(username);
    printf("\n Password:\n");
    gets(pwd);
    if (!strcmp(username, "programmer") && !strcmp(pwd, "123456")) {
        printf("Login Success!\n");
    } else if (!strcmp(username, "programmer") || !strcmp(pwd, "123456")) {
        if (!strcmp(username, "123456")) {
            printf("\nUsername..\n");
        } else {
            printf("\n Password..\n");
        }
    }
}
```
