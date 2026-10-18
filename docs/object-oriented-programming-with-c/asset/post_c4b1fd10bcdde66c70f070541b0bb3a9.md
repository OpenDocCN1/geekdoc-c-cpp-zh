
## Exception Handling

### Key Concepts

- Errors and exceptions
- Throwing mechanism
- Multiple catching
- Rethrowing exceptions
- Exception handling mechanism
- Catching mechanism
- Catching all exceptions
- Restricting exceptions thrown

### 13.1 Introduction

We know that it is very rare that a program works correctly first time. It might have bugs. The two most common types of bugs are *logic errors* and *syntactic errors*. The logic errors occur due to poor understanding of the problem and solution procedure. The syntactic errors arise due to poor understanding of the language itself. We can detect these errors by using exhaustive debugging and testing procedures.

We often come across some peculiar problems other than logic or syntax errors. They are known as *exceptions*. Exceptions are run time anomalies or unusual conditions that a program may encounter while executing. Anomalies might include conditions such as division by zero, access to an array outside of its bounds, or running out of memory or disk space. When a program encounters an exceptional condition, it is important that it is identified and dealt with effectively. ANSI C++ provides built-in language features to detect and handle exceptions which are basically run time errors.

Exception handling was not part of the original C++. It is a new feature added to ANSI C++. Today, almost all compilers support this feature. C++ exception handling provides a type-safe, integrated approach for coping with the unusual predictable problems that arise while executing a program.

### 13.2 Basics of Exception Handling

![](img/62b7c32e48e4f960a8dc2825a7119fb2_556_0.png)

C++ exception handling mechanism is basically built upon three keywords, namely, try, throw, and catch. The keyword try is used to preface a block of statements (surrounded by braces) which may generate exceptions. This block of statements is known as try block. When an exception is detected, it is thrown using a throw statement in the try block. A catch block defined by the keyword catch 'catches' the exception 'thrown' by the throw statement in the try block, and handles it appropriately. The relationship is shown in Fig. 13.1.

The catch block that catches an exception must immediately follow the try block that throws the exception. The general form of these two blocks is as follows:

```cpp
try
{
    ......
    ......
    throw exception;  // Block of statements which
                      // detects and throws an exception
    ......
}
catch(type arg)       // Catches exception
{
    ......
    ......
    // Block of statements that
    // handles the exception
    ......
}
......
......
```

When the **try** block throws an exception, the program control leaves the **try** block and enters the **catch** statement of the catch block. Note that exceptions are objects used to transmit information about a problem. If the type of object thrown matches the *arg* type in the **catch** statement, then the catch block is executed for handling the exception. If they do not match, the program is aborted with the help of the **abort()** function which is invoked by default. When no exception is detected and thrown, the control goes to the statement immediately after the catch block. That is, the catch block is skipped. This simple try-catch mechanism is illustrated in Program 13.1.

#### Program 13.1 Try Block Throwing an Exception

```cpp
#include <iostream>

using namespace std;
int main()
{
    int a,b;
    cout << "Enter Values of a and b \n";
    cin >> a;
    cin >> b;
    int x = a-b;
    try
    {
        if(x != 0)
        {
            cout << "Result(a/x) = " << a/x << "\n";
        }
        else // There is an exception
        {
            throw(x); // Throws int object
        }
    }
    catch(int i) // Catches the exception
    {
        cout<<"Exception caught: DIVIDE BY ZERO\n";
    }
    cout << "END";

    return 0;
}
```

**First Run**

```text
Enter Values of a and b
20 15
Result(a/x) = 4
END
```

**Second Run**

```text
Enter Values of a and b
10 10
Exception caught: DIVIDE BY ZERO

END
```

The program detects and catches a division-by-zero problem. The output of first run shows a successful execution. When no exception is thrown, the **catch** block is skipped and execution resumes with the first line after the **catch**. In the second run, the denominator x becomes zero and therefore a division-by-zero situation occurs. This exception is thrown using the object **x**. Since the exception object is an **int** type, the **catch** statement containing **int** type argument catches the exception and displays necessary message.

Most often, exceptions are thrown by functions that are invoked from within the **try** blocks. The point at which the **throw** is executed is called the *throw point*. Once an exception is thrown to the catch block, control cannot return to the throw point. This kind of relationship is shown in Fig. 13.2.

**Fig. 13.2** Function invoked by try block throwing exception

The general format of code for this kind of relationship is shown below:

```cpp
type function(arg list)    // Function with exception
{
    ......
    ......
    throw(object);    // Throws exception
    ......
}
......
......
```

#### Program 13.2

```cpp
#include <iostream>

using namespace std;

void divide(int x, int y, int z)
{
    cout << "We are inside the function\n";
    if((x-y) != 0)
    {
        cout << "Result = " << z/(x-y) << "\n";
    }
    else                 // There is a problem
    {
        throw(x-y);   // Throw point
    }
}
int main()
{
    try
    {
        cout << "We are inside the try block\n";
        divide(10,20,30);          // Invoke divide()
        divide(10,10,20);          // Invoke divide()
    }
    catch(int i)                  // Catches the exception
    {
        cout << "Caught the exception \n";
    }
    return 0;
}
```

The output of the Program 13.2 would be:

```text
We are inside the try block

We are inside the function
Result = -3

We are inside the function
Caught the exception
```

The *type* indicates the type of exception that a catch block handles. The parameter *arg* is an optional parameter name. Note that the exception-handling code is placed between two braces. The **catch** statement catches an exception whose type matches with the type of **catch** argument. When it is caught, the code in the catch block is executed.

If the parameter in the **catch** statement is named, then the parameter can be used in the exception-handling code. After executing the handler, the control goes to the statement immediately following the catch block.

Due to mismatch, if an exception is not caught, abnormal program termination will occur. It is important to note that the **catch** block is simply skipped if the **catch** statement does not catch an exception.

### Multiple Catch Statements

It is possible that a program segment has more than one condition to throw an exception. In such cases, we can associate more than one **catch** statement with a **try** (much like the conditions in a **switch** statement) as shown below:

```cpp
try
{
    // try block
}
catch(type1 arg)
{
    // catch block1
}
catch(type2 arg)
{
    // catch block2
}
```

When an exception is thrown, the exception handlers are searched _in order_ for an appropriate match. The first handler that yields a match is executed. After executing the handler, the control goes to the first statement after the last `catch` block for that `try`. (In other words, all other handlers are bypassed). When no match is found, the program is terminated.

It is possible that arguments of several `catch` statements match the type of an exception. In such cases, the first handler that matches the exception type is executed.

Program 13.3 shows a simple example where multiple catch statements are used to handle various types of exceptions.

#### Program 13.3 Multiple Catch Statements

```cpp
#include <iostream>

using namespace std;

void test(int x)
{
    try
    {
        if(x == 1) throw x;        // int
        else if(x == 0) throw 'x'; // char
    }
}
```
