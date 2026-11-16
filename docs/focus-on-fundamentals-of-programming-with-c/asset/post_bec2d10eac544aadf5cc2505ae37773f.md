
Of course you might want to switch the order of foo1() and foo2() in your program and all would be well. However, in a large program with dozens of functions, it might not be so easy to order the functions properly. With the use of function prototypes, we never have to worry about the order of our functions.

One last reason for the use of function prototypes deals with the building of larger programs and linking source codes together. This will be a topic for discussion at a later time.

## Function Return Values

Note that even though a function returns a value, a program need not make use of it:

```c
while (...) {
    :
    getchar(); // get a character and do nothing with it
    c = getchar(); // get another character and assign to c
    :
}
```

## void Return Values and void Parameter List

If a function does not return any value, its return type should be specified as void. The void specifier informs the compiler that a function does not return a value. In a sense, the void data type is actually defining the absence of a data type and a function declared to be of type void has no return value and cannot be used in an expression as if it does.

```c
void printHeader(void) {
    printf("Program Number 1\n");
    printf("by Richard Stegman\n");
    printf("Version 1.0, released 2/12/14\n");
}
```

As you can see, this function returns no value. You can call it with the following statement:

```c
printHeader();
```

Note that you must include ( ) in the call. If you do not, the function is not called, even though it will compile correctly on many systems.

If a function is not passed any parameters (i.e., there are no formal parameters declared), void should be specified in the parameter list within the parentheses after the function name. Here is a function that accepts no values and generates and returns a random number between 0 and 255:

```c
int getRandomNumber(void) {
    return (rand() % 255);
}
```

The function header:

```c
int getRandomNumber()
```

declares the function:

```c
getRandomNumber()
```

to the rest of the program and specifies that the function will accept no parameters and will return an int result.

## Function Parameters

The value that is being passed to a function is called an *argument* or an *actual parameter*. The argument that appears in the function header is referred to as the *formal parameter*. We say that the actual parameter is passed to the formal parameter.

Function arguments are always passed *by value* in C. Each argument is evaluated and its value is used locally in place of the formal parameter in the function header. Therefore if an argument is passed to a function, the stored value of that argument will not be changed in the calling environment. For example:

```c
#include <stdio.h>

void foo(int num);

int main(void) {
    int num = 5;
    printf("%d\n", num);
    foo(num);
    printf("%d\n", num);
    return 0;
}

int foo(int num) {
    printf("%d\n", num);
    num = num + 1;
    printf("%d\n", num);
}
```

produces the following output:

```
5
6
5
5
```

If we want to pass an argument *by reference* (i.e., change the value of the argument in the function and have that new value be reflected back in the calling function), we must pass the *address* of the argument to the function, rather than the argument itself. Once the function has access to the memory location that is used to store the actual parameter, it can modify its contents, and thus modify the actual parameter.

For example:

```c
#include <stdio.h>

void foo(int *num);

int main(void) {
    int num = 5;

    printf("%d\n", num);
    foo(&num);
    printf("%d\n", num);

    return 0;
}

void foo(int *num) {
    printf("%d\n", *num);
    *num = *num + 1;
    printf("%d\n", *num);
}
```

produces the following output:

```
5
5
6
6
```

Note that the value of the actual parameter has been changed by the call to foo().

In order to pass by reference, we must first pass the address of the actual parameter to the function. This is accomplished by using the address of operator (&). When & is placed in front of a variable, it returns the address of that variable.

So in the call from main():

```c
foo(&num);
```

we are passing the address of num to function foo().

Now look at the declaration of the formal parameter for foo() in the function header. The * that appears in front of num is saying that the value being passed to foo() is actually a memory address rather than a data value. Now if we have a memory address and want to actually get to the data value stored in that memory location, we must use the indirection operator (*) to fetch it. The * is placed before the formal parameter name in every place we try and access the formal parameter in the function.

Here's a program that swaps the value of two integers passed by reference:

```c
#include <stdio.h>

void swap(int *x, int *y);

int main(void) {
    int a, b;

    a = 5;
    b = 9;

    printf("Before swap: a = %d   b = %d\n", a, b);
    swap(&a, &b);

    printf("After swap: a = %d   b = %d\n", a, b);

    return 0;
}

void swap(int *x, int *y) {
    int temp;

    temp = *x;
    *x = *y;
    *y = temp;
}
```

Our program output looks like this:

```
Before swap: a = 5   b = 9
After swap: a = 9   b = 5
```

## Pass by Reference and scanf() Function

As previously indicated, scanf() needs to know the addresses of the items to be read. Therefore the names of variables are preceded by the address-of operator, &. However, if a parameter is passed by reference to a function and that variable is used in a scanf() statement, there is no need to place the address-of operator in front of the variable. This is because the variable already represents an address due to the fact that it was passed by reference.

```c
#include <stdio.h>

void getValue(int *num);

int main(void) {
    int num;

    getValue(&num);
    printf("The Value input = %d\n", num);
    return 0;
}

void getValue(int *num) {
    printf("Enter a number: ");
    scanf("%d", num); // No address-of (&) operator required
}
```

Here's the output produced:

```
Enter a number: 35
The value input = 35
```

## Functions Revisited Homework

- 1. Write a function, `timeUpdate()`, that is passed three `int` parameters, `hour`, `min`, `sec`, representing the current time and returns the time updated by one second. The function should work with a 24-hour clock where 4:30 a.m. is represented by 4:30 and 4:30 p.m. is represented by 16:30.

- 2. Explain the output of the following program. Does interchanging the arguments in the last `printf()` statement make any difference?

```c
#include <stdio.h>

int main(void)
{
    char a = 127, b = -128;

    printf("%5d %5d %5d\n", a, a + 1, b);
    printf("%5d %5d %5d %5d\n", a, a += 1, b, a);
    return 0;
}
```

Output:
127 128 -128
127 -128 -128 -128

C doesn't specify the order in which function parameters are processed. So, some C compilers might look at the first parameter first and therefore change the value of parameters that might reference a parameter. A good rule to follow is to not have an expression in a parameter that might change the value of a parameter.

```c
void timeUpdate(int *hour, int *min, int *sec)
{
    *sec++;
    if (*sec == 60) {
        *sec = 0;
        *min++;
        if (*min == 60) {
            *min = 0;
            *hour++;
            if (*hour == 24)
                *hour = 0;
        }
    }
}
```

[Instructor's notes]
if printf evaluates the arguments from right to left, output: -128 -128 -128
if left to right, then it is as in the print. It could be also -128 -128 -128 -128
The answer is that it is unknown.

## Checking Account Lab

Construct a C program, check.c, that reads the details of a monthly checking account and outputs a bank statement summarizing these transactions. An input file, account.txt, contains a list of transactions for the checking account for one month. Each line of the input file consists of a one-character transaction code along with a double containing the amount of the transaction. Valid transaction codes are as follows:

- I : Initial balance brought forth from previous month
- D : Deposit
- C : Check

As each transaction is entered, you should output on a single line the type of transaction, the amount of the transaction (separate columns for deposits and checks), and the balance after the transaction has been processed:

| Transaction | Deposit | Check | Balance |
|---|---|---|---|
| Initial Balance | | | 478.83 |
| Deposit | 127.45 | | 606.28 |
| Deposit | 619.84 | | 1226.12 |
| Check | | 945.12 | 281.00 |
| Check | | 4.76 | 276.24 |
| ... | | | |

The bank's service charges (which should be deducted from the balance at the end of the month) are as follows:

- $3.00 per month to maintain the account.
- $0.06 for each check cashed.
- $0.03 for each deposit made.
- $5.00 overdraft whenever a check cashed brings the balance below $0.00.

Note: Do not assess the overdraft service charge when the transaction is a deposit into an overdrawn account that does not bring the balance above zero.
