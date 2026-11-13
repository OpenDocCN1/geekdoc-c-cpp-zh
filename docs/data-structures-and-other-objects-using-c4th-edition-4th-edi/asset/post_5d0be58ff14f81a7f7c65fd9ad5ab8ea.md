
why the "bug" occurs, and then "debug the program." When you have found an error, there is an impulse to dive right in and start changing code. It is tempting to look for suspicious parts of your code and change these suspects to something "that might work better." Avoid the temptation.

An impulsive change to suspicious code almost always makes matters worse. Instead, you must discover exactly why a test case is failing and limit your changes to corrections of known errors. Once you have corrected a known error, all test cases should be rerun.

Tracking down the exact reason why a test case is failing can be difficult. For large programs, tracking down errors is nearly impossible without the help of a software tool called a debugger. A debugger executes your code one line at a time, or it may execute your code until a certain condition arises. Using a debugger, you can specify what conditions should cause the program execution to pause. You can also keep a continuous watch on the location of the program execution and on the values of specified variables.

- **Debugging Tip**
  - 1. Never start changing suspicious code on the hope that the change "might work better."
  - 2. Instead, you should discover exactly why a test case is failing and limit your changes to corrections of known errors.
  - 3. Once you have corrected a known error, all test cases should be rerun.
  - Use a software tool called a debugger to help track down exactly why an error occurs.

## Self-Test Exercises for Section 1.3

- 17. List two properties of good test data.
- 18. What boundary values should you use as test inputs for the day variable in the function date_check from page 15?
- 19. Suppose you write a program that accepts as input any integer in the range -20 through 20, and outputs the number of digits in the input integer. What boundary values should you use as test inputs?
- 20. What are two rules for fully exercising code?
- 21. Suppose you write a program that accepts a single line as input, and outputs a message telling whether or not the line contains the letter A, and whether or not it contained more than three A's. What is a good set of test inputs?
- 22. Describe how a profiler and a debugger typically aid in testing and debugging programs.

## CHAPTER SUMMARY

- The first step in producing a program is to write a precise description of what the program is supposed to do.
- One good method for specifying what a function is supposed to do is to provide a precondition and postcondition for the function. These form a contract between the programmer who uses the function and the programmer who writes the function. Using the assert function to check preconditions can significantly reduce debugging time, and the assertion-checking can later be turned off if program speed is a consideration.
- Pseudocode is a mixture of C++ (or some other programming language) and English (or some other natural language). Pseudocode is used to express algorithms so that you are not distracted by details of C++ syntax.
- Understanding and using the C++ Standard Library can make program development easier. In addition, studying the data structures of the Standard Library can help you understand trade-offs between different approaches, and can guide the design and implementation of your own data structures. When you are designing your own data structures, an approach that is compliant with the Standard Library allows others to more easily understand your work, and your own work will readily benefit from other pieces of the Standard Library.
- Time analysis is an analysis of how many operations an algorithm requires. Often, it is sufficient to express a time analysis in big-O notation, which is the order of an algorithm. The order analysis is often enough to compare algorithms and estimate how running time is affected by changing input size.
- Three important examples of big-O analyses are linear (O(n)), quadratic (O(n^2)), and logarithmic (O(log n)).
- An important testing technique is to identify and test boundary values. These are values that lie on a boundary between different kinds of behavior for your program.
- A second important testing technique is to ensure that your test cases are fully exercising the code. A software tool called a profiler can aid in fully exercising code.
- During debugging, you should discover exactly why a test case is failing and limit your changes to corrections of known errors. Once you have corrected a known error, all test cases should be rerun. Use a software tool called a debugger to help track down exactly why an error occurs.

- 1. a) The potential for code reuse. b) The possibility of future changes to the program.
- 2. A function prototype consists of the return type, name, and parameter list, which are all followed by a semicolon.
- 3. The function returns 7 on July 22, 2009. On both July 30, 2009 and February 1, 2010 the function returns 0 (since July 29, 2009 has already passed).
- 4. assert (month > 0 && month <=12);
- 5. Precondition: x >= 0. Postcondition: The return value is the positive square root of x.
- 6. #include <cmath>
  Older compilers may require <math.h> instead.
- 7. using namespace std;
- 8. The modification should change only the constants at the top of the program, the function celsius_to_fahrenheit and the call to this function.
- 9. Stopping early with an error message makes debugging easier.
- 10. #define NDEBUG should appear before any include directives.
- 11. Part d is linear (i.e., O(n)); parts f and g are logarithmic (i.e., O(log n)); all of the others are quadratic (i.e., O(n^2)).
- 12. The only O(n) formula is (d).
- 13. Worst-case analysis counts the maximum required number of operations for a function. If the exact count of the number of operations cannot be determined, the number of operations may be estimated, provided that the estimate is guaranteed to be higher than the actual number of operations.
- 14. This is a nested loop in which the number of times the inner loop executes is one more than the value of the outer loop index. The inner loop statements execute n + (n + 1) + ... + 2 + 1 times. This sum is n(n + 1)/2 and gives O(n^2).
- 15. n^2 + 1; 10n + 10,000; 50 log n; 1,000,000.
- 16. Here is one implementation of the function:

  ```cpp
  int sum(int n)
  // Precondition: n >= 1.
  // Postcondition: The value returned is the
  // sum of all integers from 1 to n.
  {
   int answer;
   int i;
   answer = 0;
   for (i = 1; i <= n; ++i)
     answer += i;
   return answer;
  }
  ```

  Our solution uses answer += i, which causes the current value of i to be added to what's already in answer.
  For a time analysis, there are two assignment operations (answer = 0 and i = 1). The <= test is executed n + 1 times (the first n times it is true, and the final time, with i equal to n + 1, it is false). The ++ and += operations are each executed n times. The entire code is O(n).

- 17. Choose test data for which you know the correct output. Test inputs should include those that are most likely to cause errors.
- 18. 28, 29, 30, and 31 should be boundary values to account for the number of days in any month. 1 should also be tested as a lower boundary value, and 27 as the biggest number that cannot be the number of days in a month. To some extent, though, this is a trick question. Any time that the number of possible inputs to a function is relatively small, we'd suggest that a test program test all possible input values.

- 19. As always, 0, 1, and -1 are boundary values. In this problem, -20 (smallest value) and 20 (largest value) are also boundary values, as are 9 and 10 (since the number changes from a single digit to two digits) and -9 and -10. (By the way, this particular problem is small enough that it would be reasonable to test _all_ legal inputs, rather than testing just the boundary values.)
- 20. Make sure that each line of your code is executed at least once by some of your test data. If part of your code is sometimes skipped during execution, make sure that at least one test input skips this part of your code.
- 21. You should include an empty line (with no characters before the carriage return) and lines with only 0, 1, 2, and 3 A's. Also include a line with 4 A's (the smallest case with more than three) and a line with more than 4 A's. For the lines with 1 or more A's, include lines that have only the A's, and also include lines that have A's together with other characters. Also test the case where all the A's appear at the front or the back of the line.
- 22. A profiler can ensure that your code is being fully exercised (by printing the count of how many times each line of your code has been executed). Once an error has been noticed, a debugger can help track down the cause of the error by displaying the values of variables while the code executes one line at a time.
