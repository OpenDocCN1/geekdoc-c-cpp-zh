
```c
// Top level program, demo0.c, used to generate demo. It is made up of demo0.c
#include <stdio.h>

// function prototypes
int incrementItem(void);
int decrementItem(void);

// a global static variable
static int count = 0;

// global variables
int gVar0 = 0;
int myArray[10];

void main(void)
{
    // local declaration
    int number = 0;

    // assign a value to the global variable i
    gVar0=3;

    // This line will print 3
    printf ("The value of gVar0 is %i\n", gVar0);

    // Three values are entered into the array myArray[] and printed
    for (gVar0=0; gVar0<3; gVar0++)
    {
        myArray[gVar0]=gVar0;
    }

    for (gVar0=0; gVar0<3; gVar0++)
    {
        printf ("the value of myArray is %i\n", myArray[gVar0]);
    }

    // The function incrementItem is called to increment the variable count the results are printed
    for (gVar0=0; gVar0<3; gVar0++)
    {
        number = incrementItem();
    }

    printf ("The total number of items is: %i\n", number);
    // The function decrementItem is called to decrement the variable count and the results are printed
    for (gVar0=0; gVar0<3; gVar0++)
    {
        number = decrementItem();
    }
    printf ("The value of number is: %i\n", number);
    printf ("The value of count is: %i\n", count);
    return;
}

int incrementItem(void)
{
    count += 1;
    return count;
}

int decrementItem(void)
{
    count -= 1;
    return count;
}
```

```c
#include <stdio.h>
#define max(a,b) ((a) > (b) ? (a) : (b))

void main(void)
{
    int i = 0;
    int j = 0;
    int a = 3;
    int b = 4;
    int c = 6;
    int d = 5;

    i = max (a, b);
    j = max (c, d);
    printf ("i = %s, j = %s\\n", i, j);

    i = max(a++, b++);
    printf ("a = %s, b = %s\\n", a, b);
    j = max(c++, d++);
    printf ("c = %s, d = %s\\n", c, d);

    return;
}
```

Figure P6.2

```c
#include <stdio.h>
void main(void)
{
    int i = 0;
    unsigned char j = 0;
    char myArray[5];        // declare a character array
    for (i = 0; i < 5; i++)    // fill array with characters
    {
        // fill with the ascii characters A.F
        // 65 is the ascii value for A
        myArray[i] = 65 + i;
    }
    for (i = 0; i < 5; i++)    // display the array
    {
        printf("the value is :%c\\n", myArray[i]);
    }
    return;
}
```

Figure P6.3

```c
#include <stdio.h>
// get data from the user
char* getSelection();
void main (void)
{
    // declare variable to store the selection and a pointer to it
    char myValue;
    char* myPtr = &myValue;
    // get selection from the user
    myPtr = getSelection();
    // display the selection
    printf("the selection is: %c \n", *myPtr);
    return;
}
// prompt the user to make a selection then return a pointer the variable holding that selection
char* getSelection(void)
{
    // declare a temp place to store the selection
    char tempValue;
    char *valuePtr;
    // let valuePtr point to it
    valuePtr = &tempValue;
    // prompt for selection
    printf("Please enter a choice between 0 - 9 : ");
    // get the data
    *valuePtr = getchar();
    // display its value
    printf("You selected: %c\n", *valuePtr);
    return valuePtr;
}
```

Figure P6.4

6.6 A colleague has come to you with the code fragment in Figure P6.2. He claims that sometimes he gets the correct results and for other times he does not. Can you explain to him what is happening and why?

6.7 You find the code fragment in Figure P6.3 in a legacy application that you are working on to incorporate some new features. The current application works with no problems. After you add your modifications, the data in the array sometimes gets

corrupted. When you remove your code, everything works properly again. Can you identify and correct the problem?

6.8 A colleague has written a simple function shown in Figure P6.4 to prompt the user to make a selection as part of a new application that both you are working on. Somehow the correct data does not seem to be returned properly, even though it prints correctly in the prompting function. Can you explain to him what the problem is and how to correct it?

## The Software Side – Part 2: Pointers and Functions

### THINGS TO LOOK FOR ...

- Pointers to variables and functions.
- C functions – passing and returning by value or reference.
- How and when to pass by information value or by reference.
- Writing and working with pointers to function pointers.
- The struct data type – declaration, initialization, and accessing.
- Pointers to structs and passing structs to functions.
- Interrupting events and interrupt control flow.
- Understanding the interrupt vector table and Interrupt service routines.
- Managing interrupts – enabling, disabling, and masking.

## 7.1 INTRODUCTION

- bitwise operators,
- functions,
- pointer variables,
- structs
- pointers to functions,
- interrupting events
- interrupts

In the early days, the software for embedded applications was written either in machine code or in assembler. The C language was developed to expedite and to simplify the design and development process. Consequently, several of the features and capabilities we find in the language were targeted specifically for such applications. In this chapter, we will examine four of these: bitwise operators; functions, pointer variables, and structs. We will also look at two important uses of pointers: pointers to functions and interrupting events for accepting and managing asynchronous events originating from inside or outside of the system.

## 7.2 BITWISE OPERATORS

Bitwise operators in C are more commonly found in the embedded systems developer's tool box rather than in that of the traditional application developer's. Such operators are intended for work at the hardware level – that is, with the registers and input or output ports on a target machine.

The bitwise operators are summarized in Table 7.1.

| Operator | Meaning | Description |
|:---|:---|:---|
| >> | Logical shift right | Operand shifted positions are filled with 0's |
| << | Logical shift left | Operand shifted positions are filled with 0's |
| & | Bitwise AND | |
| \| | Bitwise inclusive OR | |
| ^ | Bitwise exclusive OR | |
| ~ | Bitwise negation | |

- unsigned integral type,
- unsigned char
- unsigned short,
- unsigned int

When working at the bit level, often _all_ of the bits in a word are important because they generally represent the state of some signal in the hardware of the machine. Consequently, the underlying operand type should be an _unsigned integral type_ such as an _unsigned char_, _unsigned short_, or _unsigned int_. We don't want one of the bits to be interpreted as a sign.

Common operations that one might perform include:

- Setting or resetting bits on a microprocessor or microcontroller output port.
- Testing status bits on input lines or in registers.
- Setting or resetting status bits as the result of some operation.
- Making comparison operations.
- Quickly performing certain multiplication or division operations.

The application of each operator is rather straightforward and follows naturally from the logical operators. Let's examine some examples of these to see how they might apply in our designs. We will first look at some simple bit manipulation operations.

### 7.2.1 Bit Manipulation Operations

The logical bitwise operators are binary operators that return the result of the logical AND, OR, or XOR of _each of the individual bits_ in the two operands. The code module in Figure 7.1 illustrates how each of these works.

_each of the individual bits_

```c
// we are working with byte sized pieces in this example

unsigned char a = 0xF3;       // a = 1111 0011 – note this is not a negative number
unsigned char b = 0x54;       // b = 0101 0100 – note this is not a positive number

unsigned char c = a & b;      // c gets a AND b
                              // a 1111 0011
                              // b 0101 0100
                              // c 0101 0000

unsigned char d = a | b;      // d gets a OR b
                              // a 1111 0011
                              // b 0101 0100
                              // d 1111 0111

unsigned char e = a ^ b;      // e gets a XOR b
                              // a 1111 0011
                              // b 0101 0100
                              // e 1010 0111

unsigned char f = ~a;         // f gets ~a
                              // a 1111 0011
                              // f 0000 1100
```

Figure 7.1 Working with Bitwise Operators

### 7.2.2 Testing, Resetting, and Setting Bits

### EXAMPLE 7.1

We can use the logical bitwise operators to determine whether a specific bit within a word is set or reset – that is, has a value of logical 1 or logical 0.

We have executed the following code to read the state of an I/O port on a microprocessor, and we wish to test whether bit 5, a status bit, is set. If it is, we wish to reset it, acknowledging the event flagged by the status bit, and we set bit 3 to initiate some action in the external device.

We will assume that the port comprises eight bits, one byte. We further assume that we have the I/O support function, *setPort()*, which we can use to perform the necessary operations on the microprocessor’s I/O ports. Such functions are found on most microprocessors that support I/O port-type operations.

The code module in Figure 7.2 illustrates several interesting techniques.

First, notice that we are using a variable *portShadow*. We use such a variable to mirror or shadow the state of all bits on an I/O port. We do this for several reasons.

As we did in the argument to the *if* clause:

```c
if (portShadow & testPattern0) // if bit 5 is set, the AND will give a
                               // nonzero result
```
