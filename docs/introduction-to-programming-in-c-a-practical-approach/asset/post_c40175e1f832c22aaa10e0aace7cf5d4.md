
## Phase 2. Editing the program

Once we know what to do, we have to think about how to translate that functionality into our chosen programming language, in this case C.

Then we will write our program in C in the editor of Visual Studio.

You can edit the program with simple text editors such as Notepad but integrated environments have multiple advantages such as indentation (which allows us to better visualize our program) or associate colors to different functionalities (to see at a glance the key words, types of data, etc)

## Phase 3. Compilation

Once the program has been edited, we compile it and see if syntactic errors occur.

Syntactic errors occur because the compiler does not understand some line that we have introduced in the source language.

The compiler is responsible for translating the source code in C in machine language.

## Phase 4. Linking

If our project consists of several files or modules, in the linking process, external references are grouped and resolved.

If our program uses external functionalities of the compiler or the operating system at this time, references to external sources are added.

After the linking process, an executable file (.exe in Windows) is produced.

## Phase 5. Execution

In this phase we can execute the executable program and see if the results match what we expected.

If we detect any error we must return to the edition and make the necessary changes.

In this phase, runtime errors may occur due to the fact that some variable takes a value outside its limits or errors in the logic of the program.

## Phase 6. Debugging

In case of errors in runtime or the expected functionality is not done correctly, we can debug the program in our programming environment.

Some useful tools are

- the option to execute the program step by step
- tell the program to stop the execution in a line of the given code.
- display of the value of the variables in real time.

## Phase 7. Testing and maintenance

The program must be tested in all possible cases, in case of detecting failures we must go again to the editing phase

Once the program is working correctly it goes to the Exploitation phase where it is executed in its real environment (e.g on the client's computer that requested the program)

Then the program enters its maintenance phase, where the client will ask us for new features or modify the program because some functionality is not to his liking.

## 7.- Modification of the program, comments and error control

We will modify our first program and we will see its effect, compile, link and execute.

We can add comments to our program with /* */or with //

Everything written in a comment will be ignored by the compiler.

It is recommended to comment our programs for a better follow-up and subsequent maintenance of the code.

We can put comments to the first example.

Now we remove the semicolon from the end of the printf and compile.

When compiling our program if it has syntactic errors, the IDE will show them to us so we can solve them.

The program can not be run until all errors have been resolved.

## 8.- Description of the part of the program

- Comments

We can put comments to indicate the name of the program, its operation, what entrances and exits will have, etc.

```
/* firstprogram.c */
```

- Preprocessing

```
#include "pch.h"
#include <iostream>
```

These lines tell the compiler where to find the definition of functions not defined in this module.

Pch.h is the so-called precompiled header and is a precompiled version of the external definitions and is used to make the compilation process faster.

- Function main

```
int main ()
```

Every program in C must include the main function that is the entry point for our program.

- Keywords

Our C program will contain a series of reserved keywords of the language that can not be used as names of other variables or functions.

- External functions printf and arguments

The printf function is an external function defined in the iostream module and added

## 11.- Basic concepts .. memory bits and bytes

Both the program and the data it uses are stored in the computer's memory.

The memory of the computer is a sequence of "boxes" to store a value of 0 or a value of 1. These "boxes" are the bits and is the minimum unit of information that a computer can store.

To improve access to memory these bits can be grouped from 8 to 8 forming a byte.

The computer's memory is expressed in multiples of one byte

1 kilobyte (or 1KB) is 1,024 bytes.
1 megabyte (or 1MB) is 1,024 kilobytes, which is 1,048,576 bytes.
1 gigabyte (or 1GB) is 1,024 megabytes, which is 1,073,741,824 bytes

## 12.- Variables. Integer and real

### Variable

A variable is a memory area of 1 or several bytes to which a name is associated so that it can be referenced in our program.

### Whole variables

Are those variables that store an integer without decimals.
variables are of type **int**

Integer e.g are integers -10, 5, 23000

### Example

```
/* using integers */
#include <stdio.h>

int main (void)
{
    /* declare the variable age as of integer type */
    int age ;

    /* assignment of an integer value to the variable */
    age = 35;

    /* show age by screen */
    printf ("My age is% d.", age);
    return 0;
}
```

### Names of variables

The names we can give to variables is a combination of numbers and letters.

Variables can not start with a number

E.g. Var1, age, name551nteger

### Character variables

Are those variables that store a character
Characters variables are of type **char**

e.g
car = 'A';

### Real Variables

These are variables that can store numbers with decimals.
The decimal point is expressed with. (not with, as in Spanish)
Real variables are of type **float**

e.g 2.9 34.89

### Example

```
/* using real */
#include <stdio.h>

int main (void)
{
        /* declare variable as an integer value */
        float myvariable;

        /* assignment of a real value to the variable */
        myvariable = 12.75;

        /* display the variable by screen */
        printf ("My variable is% f.", myvariable);
        return 0;
}
```

## 13.- Mathematical operations

### Assignment

To assign a value to a variable we can use

```
variable = value;
```

### Operations +, -, *, /

e.g

```
sum = var1 + var2;
subtraction = value - 10;
product = 20 * 22;
division = 12.2/2.5;
```

## 14.- Conversion of types

### Implicit conversion

If in an arithmetic expression there is a real this is converted to a real value

e.g
```
float vreal;
int ventera;

ventera = 5;
vreal = ventera * 10.5;
```

### Explicitly conversion

Sometimes for clarity in the code we can force conversion from one type to another

e.g
```
float vactual;
int ventera;

ventera = 5;
vreal = (float) ventera * 10.5;
```

## 15.- Example. Calculation of prices with VAT

```
/* vat.c */
int main (void)
{
    /* declare variables */
    float price_less;
    float price_with_vat;
    int vat;

    /* assignment of values, request of data to the user */
    printf ("Enter the price without VAT:");
    scanf_s ("% f", & price_less);
    printf ("\nEnter the vat to apply:");
    scanf_s ("% d", & vat);

    price_with_iva = price_less * vat/100;

    /* show data on screen */
    printf ("\nThe price with VAT is% .2f \n", price_with_vat);
    return 0;
}
```

First we declare the variables that we are going to use, price_less and price_with_vat as real and VAT as integer.

Then we ask the user to enter the price values without VAT and VAT.

To request a data to the user we can use the function scanf_s or scanf depending on the compiler version.

Once we request the data, we calculate the price with VAT and show it on the screen.

## 16.- Making decisions

In this section we will discuss how we can make decisions to define the flow
of our program.

We will learn the different sentences in C to make choices depending on
conditions.
