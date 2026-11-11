
An example:

```c
enum day {Monday,Tuesday, ... Sunday};
enum day week_st, week_end;
week_st = Monday;
week_end = Friday;
if(week_st == Tuesday)
    week_end = Saturday;
```

The compiler automatically assigns integer digits beginning with 0 to all the enumeration constants. That is, the enumeration constant value1 is assigned 0, value2 is assigned 1, and so on. However, the automatic assignments can be overridden by assigning value explicitly to the enumeration constants. For example:

```c
enum day {Monday = 1, Tuesday, ... Sunday};
```

Here, the constant Monday is assigned the value of 1. The remaining constants are assigned values that increase successively by 1.

The definition and declaration of enumerated variables can be combined in one statement. Example:

```c
enum day {Monday, ... Sunday} week_st, week_end;
```

## 4.9 DECLARATION OF STORAGE CLASS

![](img/11b034a94fc590add0a7808250a38792_146_0.png)

Variables in C can have not only *data type* but also *storage class* that provides information about their location and visibility. The storage class decides the portion of the program within which the variables are recognized. Consider the following example:

```c
/* Example of storage classes */
int m;
main()
{
    int i;
    float balance;
    ....
    ....
    function1();
}
function1()
{
    int i;
    float sum;
    ....
    ....
}
```

The variable **m** which has been declared before the **main** is called *global variable*. It can be used in all the functions in the program. It need not be declared in other functions. A global variable is also known as an *external variable*.

The variables **i**, **balance** and **sum** are called *local variables* because they are declared inside a function. Local variables are visible and meaningful only inside the functions in which they are declared. They are not known to other functions.

Note that the variable i has been declared in both the functions. Any change in the value of i in one function does not affect its value in the other.

C provides a variety of storage class specifiers that can be used to declare explicitly the scope and lifetime of variables. The concepts of scope and lifetime are important only in multifunction and multiple file programs and therefore the storage classes are considered in detail later when functions are discussed. For now, remember that there are four storage class specifiers (auto, register, static, and extern) whose meanings are given in Table 4.10.

The storage class is another qualifier (like long or unsigned) that can be added to a variable declaration as shown below:

```c
auto int count;
register char ch;
static int x;
extern long total;
```

Static and external (extern) variables are automatically initialized to zero. Automatic (auto) variables contain undefined values (known as ‘garbage’) unless they are initialized explicitly.

**Table 4.10** Storage Classes and Their Meaning

| Storage class | Meaning |
| :--- | :--- |
| **auto** | Local variable known only to the function in which it is declared. *Default is auto.* |
| **static** | Local variable which exists and retains its value even after the control is transferred to the calling function. |
| **extern** | Global variable known to all functions in the file. |
| **register** | Local variable which is stored in the register. |

## 4.10 ASSIGNING VALUES TO VARIABLES

Variables are created for use in program statements such as,

```c
value = amount + inrate * amount;
while (year <= PERIOD)
{
    ....
    ....
    year = year + 1;
}
```

In the first statement, the numeric value stored in the variable **inrate** is multiplied by the value stored in **amount** and the product is added to **amount**. The result is stored in the variable **value**. This process is possible only if the variables **amount** and **inrate** have already been given values. The variable **value** is called the *target variable*. While all the variables are declared for their type, the variables that are used in expressions (on the right side of equal (=) sign of a computational statement) *must* be assigned values before they are encountered in the program. Similarly, the variable **year** and the symbolic constant **PERIOD** in the **while** statement must be assigned values before this statement is encountered.

### 4.10.1 Assignment Statement

Values can be assigned to variables using the assignment operator = as follows:

```
variable_name = constant;
```

We have already used such statements in Chapter 3. Further examples are:

```
initial_value     = 0;
final_value       = 100;
balance           = 75.84;
yes               = 'x';
```

C permits multiple assignments in one line. For example

```
initial_value = 0; final_value = 100;
```

are valid statements.

An assignment statement implies that the value of the variable on the left of the ‘equal sign’ is set equal to the value of the quantity (or the expression) on the right. The statement

```
year = year + 1;
```

means that the ‘new value’ of **year** is equal to the ‘old value’ of **year** plus 1.

During assignment operation, C converts the type of value on the right-hand side to the type on the left. This may involve truncation when real value is converted to an integer.

It is also possible to assign a value to a variable at the time the variable is declared. This takes the following form:

```
data-type variable_name = constant;
```

Some examples are:

```
int final_value       = 100;
char yes              = 'x';
double balance        = 75.84;
```

The process of giving initial values to variables is called *initialization*. C permits the *initialization* of more than one variables in one statement using multiple assignment operators. For example the statements

```
p = q = s = 0;
x = y = z = MAX;
```

are valid. The first statement initializes the variables **p**, **q**, and **s** to zero while the second initializes **x**, **y**, and **z** with **MAX**. Note that **MAX** is a symbolic constant defined at the beginning.

Remember that external and static variables are initialized to zero by *default*. Automatic variables that are not initialized explicitly will contain garbage.

## WORKED-OUT PROBLEM 4.2

The program in Fig. 4.8 illustrates the use of `scanf` function.

The first executable statement in the program is a `printf`, requesting the user to enter an integer number. This is known as "prompt message" and appears on the screen like

```
Enter an integer number
```

As soon as the user types in an integer number, the computer proceeds to compare the value with 100. If the value typed in is less than 100, then a message

```
Your number is smaller than 100
```

is printed on the screen. Otherwise, the message

```
Your number contains more than two digits
```

is printed. Outputs of the program run for two different inputs are also shown in Fig. 4.9.

```
Program

main()
{
    int number;

    printf("Enter an integer number\n");
    scanf ("%d", &number);

    if ( number < 100 )
        printf("Your number is smaller than 100\n\n");
    else
        printf("Your number contains more than two digits\n");
}

Output

Enter an integer number
54
Your number is smaller than 100
Enter an integer number
108
Your number contains more than two digits
```

**Fig. 4.8** *Use of scanf function for interactive computing*

Some compilers permit the use of the 'prompt message' as a part of the control string in **scanf**, like

```
scanf("Enter a number %d",&number);
```

In Fig. 4.8 we have used a decision statement **if...else** to decide whether the number is less than 100.

## WORKED-OUT PROBLEM 4.3

Program in Fig. 4.9 shows typical declarations, assignments and values stored in various types of variables.

The variables **x** and **p** have been declared as floating-point variables. Note that the way the value of 1.234567890000 that we assigned to **x** is displayed under different output formats. The value of **x** is displayed as 1.234567880630 under %.12lf format, while the actual value assigned is 1.234567890000. This is because the variable **x** has been declared as a **float** that can store values only up to six decimal places.

The variable **m** that has been declared as **int** is not able to store the value 54321 correctly. Instead, it contains some garbage. Since this program was run on a 16-bit machine, the maximum value that an int variable can store is only 32767. However, the variable **k** (declared as **unsigned**) has stored the value 54321 correctly. Similarly, the **long int** variable **n** has stored the value 1234567890 correctly.

The value 9.87654321 assigned to **y** declared as double has been stored correctly but the value is printed as 9.876543 under %lf format. Note that unless specified otherwise, the **printf** function will always display a **float** or **double** value to six decimal places. We will discuss later the output formats for displaying numbers.
