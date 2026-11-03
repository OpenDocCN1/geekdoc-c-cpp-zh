
| Format specifier | Description |
|---|---|
| `%e` | exponential notation. |
| `%g` | float or exponential notation. |
| `%o` | print an int argument in octal (base 8) |
| `%x` | print an int argument in hexadecimal (base 16) |
| `%X` | print an int argument in hexadecimal (base 16) in uppercase |
| `%c` | print a character. |
| `%s` | print a string. |

## Escape sequences

Certain non printable characters, which are used in the `printf()` function are called as escape sequences. Escape sequences always begin with backslash (`\`). Commonly used escape sequences are:

### Escape sequences

| Escape sequence | Description |
|---|---|
| `\a` | Bell beep. |
| `\b` | back space (brings cursor one position left) |
| `\f` | form feed (ejects current paper from printer and loads a new one) |
| `\n` | New line character. |
| `\r` | carriage return (brings cursor to the beginning of the line) |
| `\t` | Horizontal tab. |
| `\v` | Vertical tab. |
| `\\` | To print backslash. |
| `\"` | To print double quotations. |
| `\'` | To print single quotations. |
| `\?` | To print question mark. |
| `\0` | Null (End of string) |

![](img/3a2b6e5e90a58a56458b0539952c0cd2_41_0.png)

## Operators

Operators can be used to perform the required computations on the values.

### Types of operators

There are three types of operators:

- 1. Unary Operator: Operators which work one operand only.
- 2. Binary Operator: Operators which work on two operands.
- 3. Ternary Operator: Operators which work on three operands.

### The Rule of Precedence

Each operator in C has precedence associated with it. This precedence is used to determine how an expression involving more than one operator are evaluated.

There are distinct levels of precedence and an operator may belong to one of the levels. The operators at the higher level of precedence are evaluated first.

### The Rule of Associativity

The operators of the same precedence are evaluated either from left to right or from right to left, depending on the level. This is known as the Associativity property of an operator. There are 45 operators in C:

### Classes of operators

Operators are divided into mainly 9 classes:

- 1. Arithmetic operator.
- 2. Unary operators.
- 3. Relational operators.
- 4. Assignment operators.
- 5. Equality operators.
- 6. Logical operators.
- 7. Conditional operators.
- 8. Bitwise operators.
- 9. Comma operators.

| Rank | Operators | Descriptions | Associativity |
|------|-----------|--------------|--------------|
| 1 | `( )` | Function call. | Left to right. |
| 1 | `[ ]` | Array element reference | |
| 1 | `->` | Structure operator (used between pointer and member) | |
| 1 | `.` | Structure operator (used between object and member) | |
| 2 | `-` | Unary minus | Right to left. |
| 2 | `+` | Unary plus | |
| 2 | `++` | Increment | |
| 2 | `--` | Decrement | |
| 2 | `!` | Logical not | |
| 2 | `~` | One’s complement | |
| 2 | `*` | Value at address (used with pointers) | |
| 2 | `&` | Address of | |
| 2 | `sizeof` | Sizeof | |
| 2 | `(type)` | Typecasting | |
| 3 | `*` | Multiplication | Left to right. |
| 3 | `/` | Division | |
| 3 | `%` | Modulus | |
| 4 | `+` | Addition | Left to right. |
| 4 | `-` | Subtraction | |
| 5 | `<<` | Left Shift | Left to right. |
| 5 | `>>` | Right Shift | |
| 6 | `<` | Less than | Left to right. |
| 6 | `<=` | Less than equal | |
| 6 | `>` | Greater than | |
| 6 | `>=` | Greater than equal | |
| 7 | `==` | Equality (conditions) | Left to right. |
| 7 | `!=` | Not Equal | |
| 8 | `&` | Bitwise AND | Left to right. |
| 9 | `^` | Bitwise XOR | Left to right. |
| 10 | `\|` | Bitwise OR | Left to right. |
| 11 | `&&` | Logical AND | Left to right. |
| 12 | `\|\|` | Logical OR | Left to right. |
| 13 | `?:` | Condition Operators | Right to left. |
| 14 | `=, *=, /=, %=, +=, -=, &=, ^=, \|=, <<=, >>=` | Assignment operators | Right to left. |
| 15 | `,` | Comma operator | Left to right. |

### 1. Arithmetic operator

These operators include `+`, `-`, `*`, `/`, `%`; the `+` and `-` operators here are used to add and subtract two operands respectively. `*` is used to multiply while `/` is used to divide.

```
int i=2,j=3,k,l;
float a,b;
k=i/j*j;
l=j/i*i;
a=i/j*j;
b=j/i*i;
printf("%d, %d, %f, %f",k,l,a,b);
Output:- 0, 2, 0.000000, 2.000000
```

`%` is called modulus operator, this operator is used to calculate remainder.

```
int a=5,b=3,c;
c=a%b;
printf("%d", c);
Output: 2
```

> Note: The modulus operator does not work on floating numbers.

### 2. Unary operators

`+`, `-`, `++`, `--`, `sizeof`, `(typecasting)` The `+` and `-` in the unary operators are used to show the sign of the numbers. The `++` operator is used to add 1 to the variable.

```
int a=5,b=4;
a++;
b--;
printf("%d,%d",a,b);
```

**Output:- 6, 3**

If we use `a++` or `++a` both will increase the value of `a` by 1. `a++` is called **postfix** while `++a` is called **prefix**.

### Postfix

```
int a=5,b;
b=a++;
printf("%d, %d",a,b);
Output:- 6,5
```

```
int i=3;
i=i++;
printf("%d",i);
Output:- 4
```

### Prefix

```
int a=5,b;
b=++a;
printf("%d, %d",a,b);
Output:- 6,6
```

```
int i=2;
printf("%d %d",++i, ++i);
```

- 1. 3 4
- 2. 4 3
- 3. 4 4
- 4. Output may vary from compiler to compiler.

Output:- b

### 3. Relational operators

`<`, `>`, `<=`, `>=` These operators are boolean operators (those operators which give answer in 1 or 0. Here 1 is considered true and 0 is false).

```
int x=10,a,b;
a=x>2;
b=x<2;
printf("%d, %d",a,b);
Output:- 1,0
```

```
int x=10,y=20,z=5,i;
i=x<y<z;
printf("%d",i);
```

- 1. 1
- 2. 0
- 3. Error
- 4. None of the above

Output:- a

### 4. Assignment operator

`=`, `+=`, `-=`, `*=`, `/=`, `%=` These operators are used to assign value to a variable.

```
a=5; /* assigning 5 to variable a */
a=5+2; /*valid*/
a=b; /*valid*/
5=a; /*invalid*/
a+b=5; /*invalid*/
```

The other operators of assignment are used for doing an arithmetic operation on a variable and then assigning the value to the same variable:

- `a+=5;` is equivalent to `a=a+5`
- `a-=5;` is equivalent to `a=a-5`
- `a*=5;` is equivalent to `a=a*5`
- `a/=5;` is equivalent to `a=a/5`
- `a%=5;` is equivalent to `a=a%5`

### 5. Equality operator - ==, !=

These two operators are used to check whether the given expression has the right and left sides equal or not. This operator is also a Boolean operator; it also gives answer in 0 or 1.

```
int a,b,c=5;
a==5;
b!=2;
printf("%d, %d",a,b);
```

Output:- 1,0

### 6. Logical Operator - &&, ||, !

These operators are also Boolean operators. `&&` and `||` operator are used with two expressions. These expressions generally have either relational operators or equality operators in them.

| Expression 1 | Expression 2 | && | \|\| |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 1 |
| 0 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |

The NOT operator is used to reverse the expression:

| Expression | ! |
|---|---|
| 0 | 1 |
| 1 | 0 |

```
int a=10,b=5,c,d;
c= a>3 && b!=3;
d= (a==10 || b>20);
printf("%d, %d",c,d);
Output:- 1, 1
```

### Using the short circuit operator

```
int a=5,b=4,c;
c= (b == 3 && a++);
printf("%d, %d, %d", a,b,c);
Output:- 5, 4, 0
```

Now let us try to understand this output, in the expression there are four types of operators, `b == 3` has equality operator. `a++` is a unary operator. These two expressions are connected to each other with a logical AND. And at last value is assigned to variable `c`.

In this expression `b == 3` is a false expression thus would give 0. The next operator is a logical AND, this operator works on two different expressions (AND gives answer as 1 only if both the expressions are true) the first one being `b == 3` and the second one `a++`. The first expression for AND is false so it will not evaluate the next expression to speed up the execution of the program.

```
int i=3,j=2,k=0,m;
m = ++i && ++j || ++k;
printf("%d %d %d %d", i , j, k,m);
Output:- 4 3 0 1
```

```
int i=3,j=2,k=0,m;
m = ++j && ++i || ++k;
printf("%d %d %d %d", i , j, k,m);
Output:- 4 3 0 1
```

```
int i=3,j=2,k=0,m;
m = ++i || ++j && ++k;
printf("%d %d %d %d", i , j, k,m);
Output:- 4 2 0 1
```

```
int i=3,j=2,k=0,m;
m = ++i && ++j && ++k;
printf("%d %d %d %d", i , j, k,m);
```

### 7. Conditional Operator

This is the only ternary type of operator in C. It works on three operands. This class of operators is a set of two operators (`?`) and (`:`) which work together. Let us understand the syntax of this operator first:

```
Condition ? true statement : false statement;
```

The above expression says if condition is true i.e. if it returns a non zero value, then the value returned will be true statement, otherwise the value returned will be false statement.
