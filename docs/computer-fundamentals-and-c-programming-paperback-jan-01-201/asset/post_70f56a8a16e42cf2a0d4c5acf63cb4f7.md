
## 5 Data—Variables and Constants

### WHAT TO LEARN

- Concept of data held in *variables and constants*.
- Classification of data into *fundamental* and *derived* types.
- Attributes of the *integer* and *floating point* data types.
- Why the char data type is special.
- How attributes of constants differ from variables.
- Overview of *arrays* and *strings* as derived data types.

### 5.1 PROGRAM DATA

We deal with data in everyday life. Data often represent the attributes of real-life objects—like name, weight, quantity or price. Because computer programs are often closely linked with real-life situations, they need data too. In fact, it is impossible to devise a meaningful program that doesn’t need data. Even though instructions make a program do all the work, it’s the data that make the same program behave in different ways.

A program must know the address in memory of every piece of data that it handles. When a program encounters the variable x, it can evaluate this variable only if it knows the memory location of x. As a programmer, you need not know the address of this location or the register where it is moved to because the compiler provides this information in the executable. Keep in mind that you are learning to use C and not assembly language.

### 5.1.1 Variables and Constants

Program data occur in the form of *variables* and *constants*. A variable has a name that is assigned a value. This value is stored in memory and can change while the program is running. We used the variables area, your_number and counter in the programs of Chapter 4. The name used to access a variable is also known as an *identifier*. (Arrays and functions also have names, hence they too are identifiers.)

Constants represent data that don’t change. In the expression (fahrenheit - 32) / 9.0, both 32 and 9.0 are constants. The first argument used with **printf** is often a string constant, say, "Printing ASCII list". Like variables, constants also occupy space in memory. These constants have no names, but later in the chapter we'll encounter constants that have names. We'll also have a look at variables that behave like constants.

### 5.1.2 Data Types

Because both numeric and string data are stored as binary numbers, how does a program distinguish between them? C is a *typed* language, which means that every data item—variable or constant—has a type associated with it. To consider variables first, its type is clearly visible in the declaration:

```c
int counter;
```

The compiler identifies the type as int, i.e. integer, and allocates *at least* 2 bytes of memory for the variable named counter. int is one of several data types in C. The highlight on “at least” signifies the inability of C to specify exact sizes for variables and constants (and we’ll soon know why). All constants (like 100, 3.142, 'A', etc.) also have data types and we must know them.

### 5.1.3 Data Sources

A program obtains its data from different sources, and the C language has different constructs for handling these sources. We have already dealt with the first two of the following three sources in Chapter 4:

- Embedded in the program (as variables and constants).
- User input captured by functions like **scanf** (a feature of interactive programs).
- External files that are read by file-related functions supported by C.

There is at least one more source of data (command-line arguments), but we'll postpone discussions on it until we have understood arrays and strings. Files are also taken up later, so we will stick to the first two data sources for the time being.

### 5.2 VARIABLES

A *variable* is a name given to a memory location that is accessed by that name to fetch or set a value at that location. Variable usage is either mandatory or compelling. For instance, if a **while** loop has to execute a finite number of times, you need a variable to determine when the loop will terminate (mandatory). On the other hand, if the rupee-dollar conversion rate is used multiple times in a program, then this value is better stored in a variable (compelling). Here, the variable behaves like a constant while the program is running.

### 5.2.1 Naming Variables

The rules for framing variable names apply to all identifiers, which include arrays and functions. A variable name can begin with a letter or the underscore ( _ ) character, but the remaining part of the name can comprise only the following characters:

- Letters (both lower- and uppercase)
- Digits
- The underscore (_) character. Note that this is different from the hyphen (-) which is available on the same key as the _ on your PC or laptop.

A variable name thus cannot begin with a digit. The names `rate1` and `_rate1` are valid but not `1rate`. Variable names are also case-sensitive; `rate1` and `RATE1` are two separate variables. Here are some examples of valid identifier names:

```c
x    ABC    name024    sampling_speed    _month    __file
```

Under C89 (the first C standard from ANSI), the first 31 characters of an identifier are significant. The remaining characters are ignored by the compiler. The following keywords used in C cannot be used as variable names:

```c
auto      continue   enum       if         short      struct     unsigned
break     default    extern     int        signed     switch     void
case      do         float      long       sizeof     typedef    volatile
char      double     for        register   static     union      while
const     else       goto       return
```

The C language also uses a number of variables but they are in uppercase. To distinguish user-defined variables from the ones used by C, you should declare variables only in lowercase.

> **Tip:** Use meaningful lowercase names for variables. Names like `x` and `abc` are valid, but they don’t intuitively reveal what they represent—unlike variables like `sampling_speed` and `conversion_rate`.

### 5.2.2 Declaring Variables

A variable must be declared before use. In most cases, the declaration is made at the beginning of the program (mostly after `main`, but sometimes before `main` for global variables). The following statement declares a variable named `bits_per_sec`:

```c
int bits_per_sec;                         // shows declaration is a statement
```

Here, the variable `bits_per_sec` has the type `int`, one of the integer types supported by C. On seeing this type, the compiler allocates at least two bytes in memory for `bits_per_sec`. It also notes the starting address of that memory location so it knows where to look up when encountering expressions that use the variable. We have still not explained the significance of the highlight on the words "at least."

Using the comma as delimiter, multiple declarations can be made in a single statement provided the type is the same:

```c
int bits_per_sec, sampling_speed;          // Variables must have same type
```

On modern machines, an `int` variable uses 4 bytes of memory, which is also the size of the word. However, when the CPU extracts these 32 bits from memory it must also know that these bits have

```c
int width = 5;
int area = LENGTH * width;
printf("Area = %d\n", area);
return 0;
}
```

4.2 Locate the syntax errors in the following code segment:

```c
int X, int Y;
scanf('%d', X);
if x < 0
    printf('Only positive integers\n');
else {
    Y = X * X;
    printf('Value of Y = ', Y);
}
```

4.3 Write a program that accepts two integers from the keyboard and prints their average. Replace the sequence `int main(void)` with `main()` and drop the `return` statement. Does the program still compile and execute properly?

4.4 The following code section compiles correctly but doesn’t work properly. What is wrong with it?

```c
int x;
while (x < 10)
    printf("This statement is executed ten times\n");
printf("Quitting ...\n");
```

4.5 Write a program that uses a `while` loop to print the integers from 1 to 10. If you replace the `<` operator with `<=`, what else do you need to do to obtain the same output?

4.6 What is the following program meant to display? Now try out the following:

- (i) Remove the function declaration. Does the program compile?
- (ii) Change the function arguments from `int` to `float`. How does the output change and why?

```c
#include <stdio.h>
float func(int x, int y);           /* Function declaration */
int main(void)
{
    float result;
    result = func(5, 8);             /* Function return value saved here ... */
    printf("%f\n", result);
    printf("%f\n", func(5.5, 8.5)); /* ... but not here */
    return 0;
}
float func(int x, int y)             /* Function definition */
{
    float z;
    z = (x + y) / 2.0;              /* The / is operator for division */
    return z;
}
```
