# Recursion and Induction

Let us prove (somewhat) rigorously that the recursive number-printing program works. To do so, we'll use a proof by induction.

Theorem 1.4 The recursive number-printing algorithm is correct for n >= 0.

Proof (By induction on the number of digits in n) First, if n has one digit, then the program is trivially correct, since it merely makes a call to printDigit. Assume then that printout works for all numbers of k or fewer digits. A number of k + 1 digits is expressed by its first k digits followed by its least significant digit. But the number formed by the first k digits is exactly [n/10], which, by the inductive hypothesis, is correctly printed, and the last digit is n mod 10, so the program prints out any (k + 1)-digit number correctly. Thus, by induction, all numbers are correctly printed.

This proof probably seems a little strange in that it is virtually identical to the algorithm description. It illustrates that in designing a recursive program, all smaller instances of the same problem (which are on the path to a base case) may be assumed to work correctly. The recursive program needs only to combine solutions to smaller problems, which are “magically” obtained by recursion, into a solution for the current problem. The mathematical justification for this is proof by induction. This gives the third rule of recursion:

+   3. Design rule. Assume that all the recursive calls work.

This rule is important because it means that when designing recursive programs, you generally don’t need to know the details of the bookkeeping arrangements, and you don’t have to try to trace through the myriad of recursive calls. Frequently, it is extremely difficult to track down the actual sequence of recursive calls. Of course, in many cases this is an indication of a good use of recursion, since the computer is being allowed to work out the complicated details.

The main problem with recursion is the hidden bookkeeping costs. Although these costs are almost always justifiable, because recursive programs not only simplify the algorithm design but also tend to give cleaner code, recursion should not be used as a substitute for a simple for loop. We’ll discuss the overhead involved in recursion in more detail in Section 3.6.

When writing recursive routines, it is crucial to keep in mind the four basic rules of recursion:

+   1. Base cases. You must always have some base cases, which can be solved without recursion.

+   2. Making progress. For the cases that are to be solved recursively, the recursive call must always be to a case that makes progress toward a base case.

+   3. Design rule. Assume that all the recursive calls work.

+   4. Compound interest rule. Never duplicate work by solving the same instance of a problem in separate recursive calls.