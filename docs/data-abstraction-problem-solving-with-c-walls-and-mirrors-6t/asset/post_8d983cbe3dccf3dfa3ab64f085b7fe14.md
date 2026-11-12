
```
G > HIGH_END, or N < 0) for any data line read. In this case,
the calling program should take action. The return value is
true if the data is error-free. */
```

```
bool readData(TableType incomeData)
{
   int group = -1;
   int number = -1;       // Input values
   bool dataCorrect = true; // No data error found as yet
   bool UserFinished = false;
   for (group = LOW_END; group <= HIGH_END; group++)
      incomeData[group - LOW_END] = 0;

   do
   {
      cout << "Please enter group and number of ";
      cout << "people in group, separated by a space: ";
      cin >> group >> number;

      cout << "Input line specifies that income group "
           << group << "contains " << number
           << " people.\n";
      if ((group >= LOW_END) && (group <= HIGH_END) &&
          (number >= 0))
         // Input data is valid - add it to tally
         incomeData[group - LOW_END] += number;
      else if ((group == 0) && (number == 0))
         UserFinished = true; // User signaled input is finished
      else
      {
         // Error in input data:
         // Set error flag and ignore input line
         dataCorrect = false;
      } // end if
   } while (dataCorrect && !UserFinished ); // end do-while

   return dataCorrect;
} // end readData
```

Although this input function will behave gracefully in the face of most common input errors, it is not completely fail-safe. What happens if an input line contains only one integer? What happens if an input line contains a noninteger? The function would be more fail-safe if it read its input character by character, converted the characters to an integer, and checked for the end of the input line. In most contexts, this processing would be a bit extreme. However, if the people who enter the data frequently err by typing nonintegers, you could alter the input function easily because the function is an isolated module. In any case, the function's initial comments should include any assumptions it makes about the data and an indication of what might make the program abort abnormally.

### B.5.2 Guarding Against Errors in Program Logic

Now consider the second type of error that a program should guard against: errors in its own logic. These are errors that you may not have caught when you debugged the program or that you may have introduced through program modification.

Unfortunately, a program cannot reliably let you know when something is wrong with it. (Could you rely on a program to tell you that something is wrong with its mechanism for telling you that something is wrong?) You can, however, build into a program checks that ensure that certain conditions always hold when the program is correctly implementing its algorithm. For example, all integers in the array incomeData of the previous example must be greater than or equal to zero. Although we argued that the function readData should not check the validity of the entries of incomeData instead of checking number, it could do so in addition to checking number. For example, if the function finds that an entry in the array incomeData is outside some range of believability, it can signal a potential problem to its users.

Another general way in which you should make a program fail-safe is to make each function check its preconditions. For example, consider the following function, factorial, which returns the factorial of an integer:

> Functions should enforce their preconditions

```
/* Computes the factorial of an integer.
@param n The given integer.
@pre n >= 0.
@post None.
@return n (n - 1) * ... * 1, if n > 0, or 1, if n == 0. */
int factorial (int n)
{
   int fact = 1;
   for (int i = n; i > 1; i--)
      fact *= i;
   return fact;
} // end factorial
```

The initial comments in this function contain a precondition—information about what assumptions are made—as should always be the case. The value that this function returns is valid only if the precondition is met. If n is less than zero, the function will return the incorrect value of 1.

In the context of the program for which this function was written, it may be reasonable to make the assumption that n will never be negative. That is, if the rest of the program is working correctly, it will call factorial only with correct values of n. Ironically, this last observation gives you a good reason for factorial to check the value of n: If n is less than zero, the warning that results from the check indicates that something may be wrong elsewhere in the program.

Another reason the function factorial should check whether n is less than zero is that the function should be correct outside the context of its program. That is, if you borrow the function for use in another program, the function should warn you if you use it incorrectly by passing it an n that is negative. A stronger check than simply the statement of the precondition in a comment is desirable.

> Note: A function should state its assumptions and, when possible, check whether arguments conform to these assumptions.

> Functions should check the values of their arguments

In this example, factorial could check the value of n and, if it is negative, return zero, because factorials are never zero. The program that uses factorial could then check for this unusual value. Alternatively, factorial could abort execution if its argument is negative. Many programming languages, including C++, support a mechanism for error handling called an exception. A module indicates that an error has occurred by throwing an exception. A module reacts to an exception that another module throws by catching the exception and executing code to deal with the error condition. C++ Interlude 3 provides more information about exceptions.

C++ also provides a convenient function assert(expression) that both displays an informative message and aborts a program if expression is zero. You can use assert to check for both error conditions and the validity of preconditions within your program. C++ Interlude 3 provides more information about assert.

## B.6 Debugging

No matter how much care you take in writing a program, it will contain errors that you need to track down. Fortunately, programs that are modular, clear, and well documented are generally amenable to debugging. Fail-safe techniques, which guard against certain errors and report them when they are encountered, are also a great aid in debugging.

### Use breakpoints, single-stepping, watches, and temporary cout statements to find logic errors

Without a systematic approach, finding a small mistake in a large program can indeed be a difficult task. Many people have difficulty in debugging a program, perhaps because they believe that their program is really doing what it is supposed to do. For example, on receiving an execution-time error message at line 1098, a person might say, “That’s impossible. The statement at line 1098 was not even executed, because it is in the else clause, and I am positive that it was not executed.” However, the proper approach is either to trace the program’s execution by using available debugging facilities or to add cout statements that show which part of the if statement was executed. By doing so, you verify the value of the expression in the if statement. If the expression is 0, for example, when you expect it to be 1, the next step is to determine how it became 0.

How can you find the point in a program where something becomes other than what it should be? A typical Integrated Development Environment, or IDE, allows you to trace a program’s execution either by single-stepping through the statements in the program or by setting breakpoints at which execution will halt. You also can examine the contents of particular variables by either establishing watches or inserting temporary cout statements. The key to debugging is simply to use these techniques to tell you what is going on. This may sound pretty mundane, but the real trick is to use these debugging aids in an effective manner. After all, you do not simply put breakpoints, watches, and cout statements at random points in the program and have them report random information.

### Systematically check a program's logic to determine where an error occurs

The main idea is systematically to locate the points of the program that cause the problem. A program’s logic implies that certain conditions should be true at various points in the program. If the program’s results differ from your expectations, an error occurs. To correct the error, you must find the first point in the program at which this difference is evident. By inserting either breakpoints and watches or cout statements at strategic locations of a program—such as at the entry and departure points of loops and functions—you can systematically isolate the error.

These diagnostic techniques should inform you whether things start going wrong before or after a given point in the program. Thus, after you run the program with an initial set of diagnostics, you should be able to trap the error between two points. For example, suppose that things are fine before you call method $M_f$ but that something is wrong by the time you call $M_f$. This kind of information allows you to focus your attention between these two points. You continue the process until eventually the search is limited to only a few statements. There is really no place in a program for an error to hide.

Programming Tip: A statement of truth about some aspect of a program’s logic is known as an assertion. You can express an assertion either as a comment or by using the assert macro. By including assertions in your program, you facilitate the debugging process.

The ability to place breakpoints, watches, and cout statements in appropriate locations and to have them report appropriate information comes in part from thinking logically about the problem and in part from experience. Here are a few general guidelines.
