
are from 0 to 4. So if the user inputs a value less than 0 or greater than 4, it should result in an exception. This `if` block that checks erroneous conditions must be in the `try` block because this is the piece of code that has a possibility to throw an exception.

```cpp
if(i<0 || i>4)
{
    throw i;
    cout<<"This statement will not be executed"<<endl;
}
```

The statement `throw i;` actually throws an exception. Since `i` is thrown by the `throw` statement and data type of `i` is int, a catch block that catches an int value will be correctly executed. Therefore, the control of execution is transferred to the following catch block; thereby printing a message: Invalid array index 7 (assume the user inputs a 7) on the computer screen.

```cpp
catch(int t)
{
    cout<<"Invalid array index "<<t<<endl;
}
```

> **NOTES**
>
> The `try` block terminates immediately after a `throw` statement is encountered and the control is transferred to the right `catch` block that can handle the thrown exception. Hence, the following statement in the `try` block that appears right after the `throw` statement will never be executed.
>
> ```cpp
> cout<<"This statement will not be executed"<<endl;
> ```
>
> In fact, it is not correct to write statements at this place because this part of the code is unreachable. Recent compilers remove such unreachable code automatically as a part of code optimization or generate necessary error/warning messages to the programmer highlighting such unreachable statements.

After the catch block completes its execution, the exception is considered to be handled. Hence, the program continues to execute normally after the catch block completes its execution. The following statement is written after the catch block:

```cpp
cout<<"Good Bye"<<endl;
```

It will get executed in any case, thereby printing Good Bye on the computer screen.

If the user inputs any valid value of `i` from 0 to 4, then the control of execution will never be transferred in the `if` block and hence the exception will not be thrown. This time the control is transferred in the `else` block because the user has inputted a valid index of an array, thereby executing the following statement, which prints the array element at a specific index `i`.

```cpp
cout<<"Element at position "<<i<<" is "<<a[i]<<endl;
```

Since there was no exception in the try block, the catch block will not be executed this time and the control of execution directly jumps to the first statement after the catch block, which is `cout<<"Good Bye"<<endl;`

This prints the message Good Bye on the computer screen.

> **NOTES**
>
> catch block is executed only if there is an exception generated in the try block. If there is no exception in the try block, all the catch block(s) are skipped.

> **NOTES**
>
> Always remember to check the boundary conditions before accessing elements of the array in your program to avoid occurrence of **array index out of bounds exception**. It is a good programming practice to have such proactive checks in the program that deals with arrays.

## 17.4.2 NULL pointer exception: An example

Let us assume that we have created a pointer in the program, which points to NULL and no valid data value. In this case, dereferencing a pointer makes no real sense because it is not pointing to any valid memory location. However, if the programmer tries to accidentally dereference this pointer, then the results will be erroneous, and this exception is called NULL pointer exception.

In this example, we will demonstrate two things together:

- 1. Handling of NULL pointer exception
- 2. Generating an exception in the called function and handling it in calling function

```cpp
#include<iostream.h>
void printData(int *p)
{
    if(p == NULL)
    {
        throw 0;
    }
    else
    {
        cout<<"Data is "<<*p<<endl;
    }
}
void main()
{
    int *p=0;
    int a=10;
    /*Following statement is commented*/
    //p=&a;
    try
    {
        printData(p);
    }
    catch(int x)
    {
        cout<<"NULL POINTER EXCEPTION. Pointer is "<<x<<endl;
    }
    cout<<"Good Bye"<<endl;
}
```

### Output

```text
NULL POINTER EXCEPTION. Pointer is 0
Good Bye
```

Let’s first look at the `printData()` function. The function is essentially used to print the data value pointed by the pointer passed to it. If the pointer points to NULL, it throws the exception.

```cpp
throw 0;
```

Otherwise, if the pointer does not point to NULL, then the function assumes it is pointing to a valid memory location and prints its data value using the statement:

```cpp
cout<<"Data is "<<*p<<endl;
```

The call to function `printData()` is made in the try block because there is a possibility of an exception to be generated within the `printData()` function. If the `printData()` function throws an exception, the catch block written inside `main()` will be executed, because there is no catch block present in `printData()` to handle this exception. In a worst-case scenario, if `main()` also does not have the relevant catch block, then the execution of the program will terminate abruptly. In this case, `printData()` function throws an exception using the statement:

```cpp
throw 0;
```

The value 0 is int and hence the following catch block is executed in `main()` function, thereby printing a message `NULL POINTER EXCEPTION` as seen in the output of the program.

```cpp
catch(int x)
{
    cout<<"NULL POINTER EXCEPTION. Pointer is "<<x<<endl;
}
```

After the catch block completes its execution, the exception is considered to be as handled. Hence, the program continues to execute normally after the catch block completes its execution. The following statement is written after the catch block.

### Case 2: Value of b is not zero

Let us assume the user inputs value of a as 10 and b as 2. In this case, the try block will not execute the throw statement because b is not zero. The division operation will be performed in the try block and the cout inside the try block will be executed printing the following message on the screen:

```text
Result of division is 5
```

Since there was no exception in the try block, the catch block will not be executed, thereby directly transferring the control to the first statement after the catch block. Hence, the addition will now be performed printing the following message on the screen:

```text
Result of addition is 12
```

> **NOTES**
>
> Always remember to check if denominator evaluates to zero before performing division in the program. It is a good programming practice to have such proactive checks in the program.

## 17.4.4 Multiple exceptions: An example

It is possible to have multiple catch blocks after a single try block. You may want to do this if there is a possibility of different types of exceptions being generated in the try block and each of them need a different handling process, when it occurs.

The program given below has multiple catch blocks after a single try block.

```cpp
#include<iostream.h>
void printData(int *p)
{
    if(p == NULL)
    {
        throw 0.0;
    }
    else
    {
        cout<<"Data is "<<*p<<endl;
    }
}
void main()
{
    int a,b,c,d;
    cout<<"Enter two numbers"<<endl;
    cin>>a>>b;
    int *p=NULL;
    /*Following statement is commented */
        // p=&a;
        try
        {
```

### NOTES

C++ determines which catch block to execute based on the data type of the object that is thrown. In this example, when the throw statement throws a constant 0.0, the catch block catching double type value will handle the exception. Whereas, when the throw statement throwing int is executed, the catch block catching int will handle the exception. Similarly, you can throw and catch object of any other data type including user-defined types. We have intentionally written one integer and one double catch block to differentiate the handling of each of the exceptions.

### NOTES

In the given program, we throw a dummy value of 0.0, which is by default considered as double. This value acts as a signal to the calling function that NULL pointer exception has occurred within the printData().

### NOTES

It is possible to create a generic catch block, which can handle all the exceptions that occur in the try block. Programmers can follow this approach if all exceptions are to be handled in the same way.

The syntax for creating a generic catch block is as follows:

```cpp
catch(...)
{
/*Generic catch block for all types of exceptions*/
}
```

The given program can be rewritten to have a single generic catch block instead of writing different catch blocks for different types of exceptions. In this case, no matter what type of exception occurs the control will always be transferred to a generic catch block that will handle all exceptions. The downside of this design is that you cannot have a specific handling for different types of exceptions. Given below is the program that uses a generic catch block:

```cpp
#include<iostream.h>
void printData(int *p)
{
    if(p == NULL)
    {
    throw 0.0;
    }
    else
    {
    cout<<"Data is "<<*p<<endl;
    }
}
void main()
{
int a,b,c,d;
cout<<"Enter two numbers"<<endl;
cin>>a>>b;
int *p=NULL;
/*Following statement is commented*/
// p=&a;
try
{
```
