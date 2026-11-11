# 1.4.1  Structured programming (supported by both C and C++)

Structured programming is also referred to as modular programming or procedural programming where the program to be developed is organized into different procedures. Each of the modules defined in the program is called as a *function* or a *procedure*. A structured programming paradigm solves a large problem by dividing the problem into small pieces known as functions. Each of the small pieces are considered as different problems and solved independently by writing different functions. The results produced by each of the small functions are consolidated at the end, so as to derive the solution for the large problem. For example, let us consider that we need to create a program to sort 100 numbers stored in a file in an ascending order. The structured programming may divide the large problem statement into the following functions:

+   1. Function to read the 100 numbers from the file.
+   2. Function to arrange the numbers in the ascending order.
+   3. Function to write the result back to the file.

Hence, we have now divided a large problem to sort the data in the file into three different problems as listed above.

In general, the structured programming paradigm divides the large program into different modules based on the ‘algorithm’ or the ‘function’ that the module performs. A function A can call another function B if A needs service which is offered by B. For example, if the job of function A is to calculate factorial of a number and job of function B is to perform multiplication, function A would need to call function B multiple times because factorial requires performing multiplication multiple times with different data values. Figure 1.14 shows a typical structured programming behaviour with five functions A, B, C, D and E. Execution flow with functions are explained in detail in Chapter 7, at this stage, we just define structured programming as a collection of different building blocks called as functions such that each function is dedicated to perform a specific operation. We will just note a few points about function calls at this stage:

+   1. After the ‘called function’ completes its execution, the control is ‘returned’ to the calling function. For example, function A calls function B and after function B completes the control is returned to function A. Similarly, D calls E and hence after E completes, the control is returned to D.

![](bbox=[0.269, 0.741, 0.707, 0.917])