
## Problems with Traditional Approaches

We analyze these approaches to see why we need a new approach (exception handling).

- 1. The first approach is the worst. We let the program abort without any warning.
- 2. The second approach is better; the program will still abort, but the user will be notified.
- 3. The third approach is better than the first two because the pair that would cause the program to abort is ignored, and the program continues with the rest of the data. The problem with this approach is that the code for handling an error is mingled with the productive code of the program. In other words, the problem here is *coupling*. The error-handling code is so coupled with the code to do the job that it is difficult to distinguish between them.
- 4. The fourth approach is the best, but it cannot be applied in all cases. In addition, the principle of modular programming dictates that the return value of a function be used only for one purpose, not two. In this case, one value (−1) is used to report an error; other values are used to return the result of the calculation.

### 14.1.2 Exception Handling Approach

To avoid the four problems mentioned in the previous section, C++ developed the *exception handling approach*. In this approach, the run-time system detects the error, but it does not abort the program. It lets the program handle the error.

> **In the exception handling approach, the run-time error is detected, but the program handles the error and aborts the program only if necessary.**

When using this approach, we still need to add extra code, but the code for error handling is not coupled with code that helps us follow the logic of the program. The code to detect and handle errors has a standard pattern that must be followed, and every C++ programmer should know how to handle it.

### Try-Catch Block

The exception handling approach in C++ uses what is called the **try-catch block**. This block is made of two clauses. The first clause, which is called the *try clause*, includes the code that may cause the program to abort. The run-time environment tries to execute the code. If the code can be executed, the program flow continues. If the code cannot be executed, the system *throws* an exception (an object of a fundamental type or a class), but it does not abort the program. The second clause, called the *catch clause*, lets the program handle the exception and continue with the rest of program if possible.

Figure 14.1 shows the simple *try-catch* block. Later in the chapter, we will see that *try-catch* blocks can have more than one *catch* clause.

Figure 14.2 shows the two versions of the *throw* operator. The first is used to throw an exception; the second is used to return an exception (we will discuss the second version later in this chapter).

Note that the expression shown in Figure 14.2 has no return value. It is called only for its side effect, which is throwing an exception. It is usually changed to an expression statement by adding a semicolon after the expression.

![](img/d68f6199646ca63591a6d8419e0ed4ba_682_0.png)

**Notes:** The `try` clause detects the possibility of error and throws an exception object. The `catch` clause handles the exception to prevent abortion. The two clauses must be one after the other without any code in between; they belong to the same block.

**Figure 14.1** A simple try-catch block

![](img/d68f6199646ca63591a6d8419e0ed4ba_682_1.png)

**Figure 14.2** Using a throw expression to throw an object (exception)

### Three Patterns

There are three patterns commonly used with exception handling approaches.

**First Pattern** In the first pattern, the try-catch block is completely contained in one function. If an exception is thrown, the rest of the try clause after the throw statement is ignored and control moves to the catch clause. The function continues after the catch clause unless the program is aborted in the catch clause. Figure 14.3 shows this pattern.

![](img/d68f6199646ca63591a6d8419e0ed4ba_682_2.png)

**Figure 14.3** Try-catch block in the calling function

Note that in this case the throw statement is enclosed in a try clause. This pattern is rare.

### EXAMPLE 14.5

We repeat Program 14.3 using the *try-catch* block to see the similarity between the traditional error checking and the exception handling approach (Program 14.5). Note that exception handling in this case means ignoring only the pair of integers that caused exception and continuing with the program. Later in this chapter we see that exception handling may need other actions.

### Program 14.5 Using a try-catch block

```cpp
/*************************************************************
 * A program that uses the try-catch block to detect an error
 * and throw it to be caught and handled by the program
 *************************************************************/
#include <iostream>
using namespace std;

int main()
{
    int num1, num2, result;
    for (int i = 0; i < 3; i++)
    {
        cout << "Enter an integer: ";
        cin >> num1;
        cout << "Enter another integer: ";
        cin >> num2;
        // The try-catch block
        try
        {
            if (num2 == 0)
            {
                throw 0;       // An object of type integer is thrown
            }
            result = num1 / num2;
            cout << "The result is: " << result << endl;
        }
        catch (int x)
        {
            cout << "Division by zero cannot be performed." << endl;
        }
    }
    return 0;
}
```

```text
Run:
Enter an integer: 6
Enter another integer: 5
The result is: 1
Enter an integer: 7
Enter another integer: 0
Division by zero cannot be performed.
Enter an integer: 8
Enter another integer: 2
The result is: 4
```

In this program, the *try-catch* block (lines 18 to 30) is highlighted. There are several points that we must explain. The *try* clause includes the code that we suspect will create a run-time error. We provide the logic, in this case a decision statement, to *throw* the exception. If an exception is thrown, control transfers to the *catch* clause. If this happens, the exception must be an object of a built-in type or user-defined type. We have decided to throw an object of type *int* in this case (of value 0). If no exception is thrown, lines 24 and 25 are executed and the *catch* clause is ignored. Also note that the *catch* clause looks like a function with one parameter of the type of the exception object, but it is not a function. It is a clause in the *try-catch* block. Its parameter (*x*) is a variable of type integer. The program output follows from Program 14.4.

**Second Pattern** In the second pattern, the *try-catch* block is still in *main*, but the exception is thrown in another function that is called in the *try* clause. The *throw* statement in this case is in the called function. When an exception is thrown, the rest of the code in the called function is ignored and the program flow moves to the *catch* block in the calling function. Figure 14.4 shows this pattern.

![](img/d68f6199646ca63591a6d8419e0ed4ba_684_0.png)

The second pattern is preferred because it follows the structural programming principle of dividing the tasks. The task of the operation is defined in the called function, and it will throw an exception if there is a problem. The task of exception handling is in the calling function.

When we put the *throw* statement in a function, we create two different return points in the called function. If no exception is thrown, the called function will return when it reaches the return statement and the program flow goes back to the calling function. In this case, the *catch* clause is ignored. If an exception is thrown, the called function is terminated prematurely and the program flow returns to the *catch* clause in the calling function.

Figure 14.4 demonstrates another advantage of using exception handlers. We do not have to return two values from a function, one for success and one for error. In the case of an error, the exception is thrown and the function is terminated.

Is the *throw* statement in this pattern also enclosed in a *try* clause? The answer is yes, but the inclusion is indirect. The *try* clause encloses the called function, and the called function encloses the *throw* statement.

### EXAMPLE 14.6

In this example we rewrite the previous program using the second pattern. The task of calculating the quotient belongs to a function called *quotient*, which throws an exception of type *int* if there is a problem. The *main* function is only responsible for calling the *quotient* and catching and handling the exception if thrown. Note that in this case catching the exception just means ignoring the pair of integers and continuing with the next pair. Program 14.6 shows the case.

### Program 14.6 Detecting an exception thrown by a function

```cpp
/********************************************************
 * A program that uses the try-catch block to detect an error   *
 * thrown by a function                                         *
 ********************************************************/
#include <iostream>
using namespace std;

int quotient (int first, int second);    // Function declaration

int main ()
{
   int num1, num2, result;
   for (int i = 0; i < 3; i++)
   {
      cout << "Enter an integer: ";
      cin >> num1;
      cout << "Enter another integer: ";
      cin >> num2;
      // The try-catch block
      try
      {
         cout << "Result: " << quotient (num1, num2) << endl;
```
