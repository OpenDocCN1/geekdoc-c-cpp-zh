known to other functions. Note that the variable i has been declared in both the functions. Any change in the value of i in one function does not affect its value in the other.

C provides a variety of storage class specifiers that can be used to declare explicitly the scope and lifetime of variables. The concepts of scope and lifetime are important only in multifunction and multiple file programs and therefore the storage classes are considered in detail later when functions are discussed. For now, remember that there are four storage class specifiers (auto, register, static, and extern) whose meanings are given in Table 1.12

The storage class is another qualifier (like long or unsigned) that can be added to a variable declaration as shown below:

```
auto int count;
register char ch;
static int x;
extern long total;
```

Static and external (extern) variables are automatically initialized to zero. Automatic (auto) variables contain undefined values (known as 'garbage') unless they are initialized explicitly.

Table 1.12 Storage Classes and Their Meaning

| Storage class | Meaning |
|---|---|
| auto | Local variable known only to the function in which it is declared. Default is auto. |
| static | Local variable which exists and retains its value even after the control is transferred to the calling function. |
| extern | Global variable known to all functions in the file. |
| register | Local variable which is stored in the register. |

# 1.34 ASSIGNING VALUES TO VARIABLES

Variables are created for use in program statements such as,

```
value = amount + inrate * amount;
while (year <= PERIOD)
{
    ....
    ....
}
year = year + 1;
```

In the first statement, the numeric value stored in the variable inrate is multiplied by the value stored in amount and the product is added to amount. The result is stored in the variable value. This process is possible only if the variables amount and inrate have already been given values. The variable value is called the target variable. While all the variables are declared for their type, the variables that are used in expressions (on the right side of equal (=) sign of a computational statement) must be assigned values before they are encountered in the program. Similarly, the variable year and the symbolic constant PERIOD in the while statement must be assigned values before this statement is encountered.

# 1.34.1 Assignment Statement

Values can be assigned to variables using the assignment operator = as follows:

```
variable_name = constant;
```