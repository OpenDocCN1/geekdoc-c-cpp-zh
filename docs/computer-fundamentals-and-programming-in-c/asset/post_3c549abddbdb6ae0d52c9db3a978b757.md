
**Format string** It is a group of characters that contain ordinary character string, conversion code, or control characters arranged in order so that they correspond to the respective control string variables placed next to it in printf() function.

**Precision modifier** It indicates the number of characters used after the decimal point in the output displayed. The precision option is used only with floats or strings.

**Size modifier** It precedes the conversion code and specifies the kind of data type thereby indicating the number of bytes required for the corresponding variable.

**White space** It is the blank space that causes the input stream to be read up to the next non-white-space character.

**Width modifier** When used in context with the format string, width modifier specifies the total number of characters used to display the output or to be read in.

## FREQUENTLY ASKED QUESTIONS

### 1. How can you print % character using printf()?

Conversion specifiers always start with a % character so that the printf() function can recognize them. Because a % in a control string always indicates the start of a conversion specifier, if one wants to output a % character you must use the sequence %% .

### 2. What is the return type of printf()?

The return value for printf() is incidental to its main purpose of printing output, and it usually isn't used. The return type of printf() function is int. Under ANSI C, printf() function returns the number of characters it printed. If there is an output error, printf() returns a negative value. The following program illustrates the fact:

```c
#include <stdio.h>
int main(void)
{
   int c;
   c=printf("One");
   printf("\nc = %d",c);
   return 0;
}
```

Output

```
One
c = 3
```

### 3. What is the return type of scanf()?

The scanf() function returns the number of variables that it successfully reads. If it reads no variables, which happens if you type a non-numeric string when it expects a number, scanf() returns the value 0. It returns EOF if it detects end of file. This condition can occur if we press CTRL-Z in Windows or CTRL-D in UNIX/Linux.

```c
#include <stdio.h>
int main(void)
{
   int a,b,c;
   c=scanf("%d %d",&a,&b);
   printf("\nc = %d",c);
   return 0;
}
```

Output

```
Sample run 1:
2 3
c = 2

Sample run 2:
2 a
c = 2

Sample run 3:
a b
c = 0

Sample run 4:
^z
c = -1
```

### 4. How do I write printf() so that the width of a field can be specified at run-time?

This is shown in the following program:

```c
int main( )
{
   int w, no;
   printf ("Enter number and the width for the\
number field:");
   scanf ("%d%d", &no, &w);
   printf ("%*d", w, no);
   return 0;
}
```

Here, * in the format specifier in printf() indicates that an int value from the argument list should be used for the field width.

### 5. What is EOF?

EOF is a special character called the end-of-file character. In fact, the symbol EOF is defined in <stdio.h> and is usually equivalent to the value -1. However, this is not necessarily always the case, so one should use EOF in the programs rather than an explicit value. EOF generally indicates that no more data is available from a stream. Incidentally EOF can be entered manually from the keyboard by pressing CTRL+D on a UNIX/Linux type machine or by pressing CTRL+Z on a Windows type machine.

## EXERCISES

### 1. What will be the value of each variable after the following input command?

data input: Tom 34678.2 AA4231

scanf("%s %3d %f %c %c %ld", name, &m, &x, &ch, &i, &j);
(a) name: ___________________________

## CHAPTER 10 Control Statements

### LEARNING OBJECTIVES

After studying this chapter, the readers will be able to

- discuss the meaning of a statement and a statement block
- explain decision type control constructs in C and the way these are used
- explain looping type control constructs in C and the technique of putting them to use
- discuss the use of special control constructs such as goto, break, continue, and return
- describe nested loops and their utility

### 10.1 INTRODUCTION

So far, every program in this book has executed sequentially in the order in which they appear, i.e., statements in a program are normally executed one after another until the last statement completes. A C application begins executing with the first line of the main() function and proceeds statement by statement until it reaches to the end of the main() function.

In C, any sequence of statements can be grouped together to function as a syntactically equivalent single statement by enclosing the sequence in braces. This grouping is known as statement block or compound statement. Compound statements were originally designed to make control structures simpler.

In C89, one must declare all local variables at the start of the block prior to any executable statements. However in C99, local variables can be declared at any point within the block prior to their first use.

Consider the following program that illustrates variable declaration at the beginning of a statement block.

```c
#include <stdio.h>
int main(void)
{
    int a=5;
    printf("\n a = %d", a);
    /* A statement block follows */
    {
        int b=10;
        printf("\n a = %d", a);
        printf("\n b = %d", b);
    }
}
```

b is visible only within this block.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_221_0.png)

Fig. 10.1   Program control statements/constructs in C

Several relational and logical operators are available to specify the test condition used in the control constructs of C. Relational operators are used to specify individual test expression. More than one test expression can be connected through the logical operator. Tables 10.1 and 10.2 list the several relational, equality, and logical operators used in C.

```
Variable                Variable
   OR                      OR
Expression   Relational_Operator   Expression
   OR                      OR
Constant                Constant
```

When the AND operator, &&, is used between two relational expressions, the result is true only if each of both the expressions are true by themselves. When using the OR operator, ||, the condition is true if either one or both of the two individual expressions is true.

The relational operators may be used with integer, float, double, or character operands.

The NOT operator, !, is used to change any expression to its opposite state. That is, if the expression has any nonzero value (true), !expression produces a zero value (false). If an expression is false to begin with (has a zero value), !expression is true and evaluates to 1.

**Table 10.1 Relational operators**

| To specify | Symbol used |
|---|---|
| less than | `<` |
| greater than | `>` |
| less than or equal to | `<=` |
| greater than or equal to | `>=` |

Among the relational, equality, and logical operators only the ‘!’ operator is unary; the rest are binary operators.

### EXAMPLES

1. Some examples of expressions are given below.
   - `a = 2`    `a < b + c`    `a == 3`
   - `a != 0`   `a <= b`       `a >= 2`

A test expression involving relational and/or equality and/or logical operators, yields either integer 1 or 0 after evaluation. Consider the following example programs.

**Table 10.2 Equality and logical operators**

| To specify | Symbol used |
|---|---|
| Equal to | `==` |
| Not equal to | `!=` |
| Logical AND | `&&` |
| Logical OR | `||` |
| Negation | `!` |

### 10.3 WRITING TEST EXPRESSION

Relational expression can be formed using relational operators. A relational operator takes two operands and compares them to each other, resulting in a value of true (1) or false (0). The syntax for relational expression is as follows:

2. (a)

```c
#include <stdio.h>
int main()
{
    int a=3;
    printf("\n%d",a>3);
    return 0;
}
```

Output 0

(b)

```c
#include <stdio.h>
int main()
{
    int a=3;
    printf("\n%d",a>2);
    return 0;
}
```

Output 1

The reason for the above output is that in C, false is represented by the value 0 and true is represented by the value 1 as it is a relational expression. In C, if such a value is zero, it is interpreted as a logical value false. If such a value is not zero, it is interpreted as the logical value true. The value for false may be any zero value, e.g., 0, 0.0, ‘0’ (null character) or the NULL pointer value, discussed later.
