
## External Storage Class

When a variable is declared outside a function, storage is permanently assigned to it and its storage class is _external_. It is considered _global_ and is visible to all functions declared after it. External variables can be a useful tool to transmit information across blocks and functions.

A declaration for an external variable looks just the same as a variable declaration inside a function or a block:

```c
// storage2.c

int x = 1;
int y = 2;

int main(void) {
    z = foo();
    printf("%d %d %d\n", x, y, z);
}

int foo(void) {
    int y, z;

    x = y = z = 3;
    return x + y + z;
}
```

Output:

3 2 9

Note that external variables never disappear, but may be hidden if the identifier is redefined.

Information can be passed into a function in two ways: by use of external or global variables (which are not allowed in this class) or by use of parameters. The use of parameters is the preferred method to pass information into a function. It tends to improve the modularity of the code and the possibility of undesirable side effects is reduced.

## For example:

```c
// storage3.c

int num;

int main(void) {
    num = 0;
    while (num < 3) {
        foo();
        num++;
    }
}

void foo(void) {
    num = 0;
    while (num < 5) {
        puts("Hello.");
        num++;
    }
}
```

See if you can figure out the intent of the code and the output.

We should avoid using unnecessary external or global variables for three reasons:

- 1. They take up memory during the entire time your program is executing, not just when they are needed.
- 2. Using an external or global variable where a local variable will do makes your function less general because the function relies on something that must be defined outside of itself.
- 3. Using a large number of external or global variables can lead to program errors because of unknown and unwanted side effects.

## Register Storage Class

Automatic (local) variables can be placed in the actual hardware registers of the computer by declaring them to have register storage class. This permits faster access during program execution. Register storage class is typically used for variables that are referenced often and this is an attempt to improve execution speed.

The syntax is as follows:

```c
register type name;
```

Note that only certain data types can be placed in registers:

- char
- short
- int
- unsigned char
- unsigned short
- unsigned int
- pointer variables as array parameters

Note that each machine is limited in the number of registers available for such variables. If a register is not available, this class defaults to automatic. So the implementation of register variables is machine dependent.

Also note that programs may not take the address (&) of a register variable, i.e., we cannot read into a register with `scanf()`.

Here's a program that counts to one million:

```c
// storage4.c

int main(void) {
    register int units;
    register int thousands;

    thousands = 0;
    while (++thousands <= 1000) {
        units = 0;
        while (++units <= 1000) {
        ;
        }
    }
}
```

Register variables should be declared as close to its place of use as possible to allow maximum availability of the registers. Upon block exit the registers are freed.

## Static Storage Class

Static storage class allows us to control whether the local variables retain their values between function calls. A static variable within a function is a local variable that retains its values from previous calls to that function. They are created the first time that a function is called and are not destroyed when the function is exited.

For example:

```c
void foo(void) {
    static int num = 0;
    ...
}
```

The value of num will be initialized to 0 only once when program execution begins. Here's a program to illustrate static and automatic variables:

```c
// storage5.c
int main(void) {
    int i;
    for (i = 0; i < 5; ++i) {
        foo();
    }
}

void foo(void) {
    int autoVar = 0;
    static int staticVar = 0;

    printf("Automatic = %d Static = %d\n", autoVar, staticVar);
    ++autoVar;
    ++staticVar;
}
```

Output:

```
Automatic = 0   Static = 0
Automatic = 0   Static = 1
Automatic = 0   Static = 2
Automatic = 0   Static = 3
Automatic = 0   Static = 4
```

Note that the static variable, staticVar, is initialized once and keeps its value between function calls.

So a static variable is a variable that is only seen within the function in which it is defined (like a local variable) but whose lifetime is that of the entire program (like a global variable).

## Initializing Arrays In Static Storage

C does not allow for the initialization of automatic (local) arrays. Only static or external arrays may be initialized with a list of values. Therefore, to initialize an array, it's best to declare the array as static.

If a static array is used within a function, then the initial values will be assigned to the array only once. Any changes made to the array elements will remain in effect throughout the execution of the program.

Here are some examples of initializing arrays in static storage:

```c
// storage6.c

static short digits[10] = { 0,1,2,3,4,5,6,7,8,9 };

static char msg[6] = "Hello";
```

Note that a character string always includes a null terminator ('\0') at the end.

If the array bound is greater than the number of initializers, the extra elements are initialized to 0. If no bound is given, the bound is taken to be the number of initializers.

Note that static and external variables that are not initialized will automatically be initialized to 0. Automatic and register variables that are not initialized will have unpredictable results!

| ATTRIBUTE | AUTO | EXTERN | STATIC EXTERN | STATIC INTERN | REGISTER |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Retain value upon leaving block | NO | YES | YES | YES | NO |
| Available to multiple functions | NO | YES | YES | NO | NO |
| Available to other source files | NO | YES | NO | NO | NO |
| Zero default when not initialized | NO | YES | YES | YES | NO |
| Initialized once at compile time | NO | YES | YES | YES | NO |
| Initialize arrays and structures | NO | YES | YES | YES | NO |
| Variables in machine registers | NO | NO | NO | NO | YES |

## Storage Location

C divides memory into four separate locations: Stack, Heap, Data Area, Code Area.

## High Memory

| Section | Content |
| --- | --- |
| **Stack** (changes size freely) | * C maintains stack for us<br>* automatic variables<br>* pass parameters to functions<br>* store return addresses<br>* set up at top of available memory and grows towards lower memory as it is filled |
| | v<br>^ |
| **Heap** (changes size freely) | * allocating and using memory on heap is our responsibility (malloc)<br>* starts in low memory and grows towards higher memory |
| **Data Area** (fixed in size) | * Uninitialized data<br>* uninitialized static and external variables<br>* all initialized to zero at once<br>--<br>* Initialized data<br>* initialized static and external variables<br>* initialized arrays and structures |
| **Code Area** (fixed in size) | * program code<br>* not changed when program runs |

## Low Memory

## Storage Class Homework

- 1. Answer each of the following questions with auto, extern, register, and/or static.

- a) Which storage class is used primarily to indicate that a variable or function can be shared by several files?

- b) Suppose that a variable x is to be shared by several functions in one file but hidden from functions in other files. Which storage class should x be declared to have?

- c) Which storage classes can affect the storage duration of a variable?

- 2. Given function foo() below:

```c
int foo(int i) {
    static int j = 0;
    return i * j++;
}
```

- a) What will be the value of foo(10) if foo() has never been called before?

- b) What will be the value of foo(10) if foo() has been called five times previously?
