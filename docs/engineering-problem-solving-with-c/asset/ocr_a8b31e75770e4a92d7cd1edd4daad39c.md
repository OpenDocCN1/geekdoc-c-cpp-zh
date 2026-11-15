This sequence was first described in the year 1202, and it has applications that range from biology to electrical engineering. For example, Fibonacci sequences are often used in studies of rabbit population growth.

A function to compute the \(k^{th}\) value in the Fibonacci sequence is a good candidate for a recursive function because each new value in the sequence is computed from the two previous values, as shown in the following recursive definition:

\(f(n) = \begin{cases} 1 & n=0, n=1 \\ f(n-1) + f(n-2) & n > 1 \end{cases}\)

We next provide a definition for a recursive function to compute the \(k^{th}\) term in the Fibonacci sequence.

```
/*-------------------------------------------------------------*/
/*                                                             */
/*   This function computes the kth Fibonacci                  */
/*   number using a recursive algorithm.                       */
/*                                                             */
/*-------------------------------------------------------------*/
int fibonacciR(int k)
{
   // Declare objects.
   int term = 1;

   // Compute kth Fibonacci number recursively
   if (k <= 1)
   {
      return term; //Unique solution.
   }
   return fibonacciR(k-1) + fibonacciR(k-2); //Reduce.
}
/*-------------------------------------------------------------*/
```

In the recursive function, the condition k <= 1 keeps the function from getting into an infinite loop.

# Modify 10.5

+   1. Use program chapter10_5 to compute values of 1!, 2!, and so on, until you reach the limits for long integers. What kind of error message occurred when the value of k! exceeded the limits on your system?
+   
+   2. Modify chapter10_5 so that it uses double values instead of integers to compute factorials. Explain why the number of digits of precision determines the maximum value of k! that can be correctly computed using double values. What is the maximum value of k! that can be computed using double values on your system?
+   
+   3. Write a main function to test the Fibonacci functions. What is the maximum Fibonacci value that can be correctly computed with integers on your system?