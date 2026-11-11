
The multifile program shown in Fig. 11.17 can be modified as shown in Fig. 11.18.

```c
/* file1.c */
int m; /* global variable */

main()
{
        int i;
        . . . . .
}
function1()
{
        int j;
        . . . . .
}
```

```c
/* file2.c */
extern int m;

function2()
{
        int i;
        . . . . .
}
function3()
{
        int count;
        . . . . .
}
```

**Fig. 11.18** *Another version of a multifile program*

When a function is defined in one file and accessed in another, the latter file must include a function declaration. The declaration identifies the function as an external function whose definition appears elsewhere. We usually place such declarations at the beginning of the file, before all functions. Although all functions are assumed to be external, it would be a good practice to explicitly declare such functions with the storage class **extern**.

## LEARNING OUTCOMES

- A function that returns a value can be used in expressions like any other C variable. (LO 11.1)
- A function that returns a value cannot be used as a stand-alone statement. (LO 11.1)
- Where more functions are used, they may be placed in any order. (LO 11.1)
- It is a syntax error if the types in the declaration and function definition do not match. (LO 11.2)
- It is a syntax error if the number of actual parameters in the function call do not match the number in the declaration statement. (LO 11.2)
- It is a logic error if the parameters in the function call are placed in the wrong order. (LO 11.2)
- Placing a semicolon at the end of header line is illegal. (LO 11.2)
- Forgetting the semicolon at the end of a prototype declaration is an error. (LO 11.2)
- A **return** statement can occur anywhere within the body of a function. (LO 11.2)
- A function definition may be placed either after or before the **main** function. (LO 11.2)
- A **return** statement is required if the return type is anything other than **void**. (LO 11.3)
- If a function does not return any value, the return type must be declared **void**. (LO 11.3)
- If a function has no parameters, the parameter list must be declared **void**. (LO 11.3)
- Using **void** as return type when the function is expected to return a value is an error. (LO 11.3)
- Trying to return a value when the function type is marked **void** is an error. (LO 11.3)
- Defining a function within the body of another function is not allowed. LO 11.3
- It is an error if the type of data returned does not match the return type of the function. LO 11.3
- It will most likely result in logic error if there is a mismatch in data types between the actual and formal arguments. LO 11.3
- Functions return integer value by default. LO 11.3
- A function without a return statement cannot return a value, when the parameters are passed by value. LO 11.3
- When the value returned is assigned to a variable, the value will be converted to the type of the variable receiving it. LO 11.3
- Function cannot be the target of an assignment. LO 11.3
- A function with void return type cannot be used in the right-hand side of an assignment statement. It can be used only as a stand-alone statement. LO 11.3
- A function can have more than one return statement. LO 11.3
- A recursive function must have a condition that forces the function to return without making the recursive call; otherwise the function will never return. LO 11.4
- It is illegal to use the name of a formal argument as the name of a local variable. LO 11.5
- Variables in the parameter list must be individually declared for their types. We cannot use multiple declarations (like we do with local or global variables). LO 11.5
- Use parameter passing by values as far as possible to avoid inadvertent changes to variables of calling function in the called function. LO 11.5
- Although not essential, include parameter names in the prototype declarations for documentation purposes. LO 11.5
- A global variable used in a function will retain its value for future use. LO 11.6
- A local variable defined inside a function is known only to that function. It is destroyed when the function is exited. LO 11.6
- A global variable is visible only from the point of its declaration to the end of the program. LO 11.6
- When a variable is redeclared within its scope either in a function or in a block, the original variable is not visible within the scope of the redeclared variable. LO 11.6
- A local variable declared **static** retains its value even after the function is exited. LO 11.6
- Static variables are initialized at compile time and therefore, they are initialized only once. LO 11.6
- Avoid the use of names that hide names in outer scope. LO 11.6

## KEY TERMS TO REMEMBER

- **Arguments:** Are the set of values that are passed to a function to enable the function to perform the desired task. LO 11.1
- **Block statement:** Is a set of statements enclosed within a set of braces. LO 11.1
- **Function:** Is an independently coded subprogram that performs a specific task. LO 11.1
- **Modular Programming:** Is a software development approach that organizes a large program into small, independent program segments called modules. LO 11.1
- **Calling program:** Is the program or function that calls another function. LO 11.2
- **Function body:** Contains the statement block for performing the required task. LO 11.2
- **Function type:** Specifies the type of value that the function will return. (LO 11.2)
- **Parameter list:** Is a list of variables that will receive data values at the time of function call. (LO 11.2)
- **Program definition:** Is an independent program module that is written to perform specific task. It is also referred as function definition. (LO 11.2)
- **Recursion:** Is a scenario where a function calls itself. (LO 11.4)
- **External variable:** Is a variable that is active throughout the program. It is also referred as global variable. (LO 11.6)
- **Local variable:** Is a variable that is active only within a specific function or statement block. It is also referred as internal variable. (LO 11.6)

## BRIEF CASES

### 1. Calculation of Area under a Curve [LO 11.1, 11.2, 11.3, 11.6 M]

One of the applications of computers in numerical analysis is computing the area under a curve. One simple method of calculating the area under a curve is to divide the area into a number of trapezoids of same width and summing up the area of individual trapezoids. The area of a trapezoid is given by

Area = 0.5 * (h1 + h2) * b

where h1 and h2 are the heights of two sides and b is the width as shown in Fig. 11.19.

The program in Fig. 11.21 calculates the area for a curve of the function f(x) = x² + 1 between any two given limits, say, A and B.

*Input*

- Lower limit (A)
- Upper limit (B)
- Number of trapezoids

![](img/11b034a94fc590add0a7808250a38792_430_0.png)

**Fig. 11.19** *Area under a curve*

```c
void input(void)
{
    printf("\n Enter lower limit:");
    scanf("%f", &start_point);
    printf("Enter upper limit:");
    scanf("%f", &end_point);
    printf("Enter number of trapezoids:");
    scanf("%d", &numtraps);
}
float find_area(float a, float b, int n)
{
    float base, lower, h1, h2;   /* LOCAL VARIABLES */
    float function_x(float x);    /* prototype */
    float trap_area(float h1,float h2,float base);/*prototype*/
    base = (b - a) / n;
    lower = a;
    for(lower =a; lower <= b-base; lower = lower + base)
    {
        h1  = function_x(lower);
        h2  = function_x(lower + base);
        total_area += trap_area(h1, h2, base);
    }
    return(total_area);
}
float trap_area(float height_1,float height_2,float base)
{
    float area;        /* LOCAL VARIABLE */
    area = 0.5 * (height_1 + height_2) * base;
    return(area);
}
float function_x(float x)
{
    /* F(x) = X * X + 1 */
    return(x*x + 1);
}
```

**Output**

```text
AREA UNDER A CURVE
Enter lower limit: 0
Enter upper limit: 3
Enter number of trapezoids: 30
```
