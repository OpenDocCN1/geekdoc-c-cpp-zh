
## Integer Types Have Limitations

Even when we use unsigned long long int, we still can’t calculate factorials beyond 21! This points to a weakness in procedural programming languages like C—the language is not easily extended to handle the unique requirements of various applications. Object-oriented languages like C++ are extensible. Through a language feature called classes, programmers can create new data types, even ones that could hold arbitrarily large integers.

### Self Check

1 (Fill-In) Omitting the base case or writing the recursion step incorrectly so that it does not converge on the base case will cause __________, eventually exhausting memory.

Answer: infinite recursion.

2 (Fill-In) The following code should iteratively calculate the factorial of an integer, number, but the code contains a bug:

```c
unsigned long long int factorial = 1;
for (int counter = number; counter >= 1; --counter)
    factorial * counter;
```

You can correct the bug by changing ______ to ______.

Answer: *, *=.

## 5.15 Example Using Recursion: Fibonacci Series

The Fibonacci series

0, 1, 1, 2, 3, 5, 8, 13, 21, …

begins with 0 and 1 and has the property that each subsequent Fibonacci number is the sum of the previous two Fibonacci numbers.

The series occurs in nature and, in particular, describes a form of spiral. The ratio of successive Fibonacci numbers converges to a constant value of 1.618…. This number, too, repeatedly occurs in nature and has been called the golden ratio or the golden mean. Humans tend to find the golden mean aesthetically pleasing. Architects often design windows, rooms and buildings whose length and width are in the ratio of the golden mean. Postcards are often designed with a golden mean length/width ratio.

The Fibonacci series may be defined recursively as follows:

fibonacci(0) = 0  
fibonacci(1) = 1  
fibonacci(n) = fibonacci(n − 1) + fibonacci(n − 2)

```c
// fig05_10.c
// Recursive fibonacci function.
#include <stdio.h>

unsigned long long int fibonacci(int n); // function prototype

int main(void) {
    // calculate and display fibonacci(number) for 0-10
    for (int number = 0; number <= 10; number++) {
        printf("Fibonacci(%d) = %llu\n", number, fibonacci(number));
    }

    printf("Fibonacci(20) = %llu\n", fibonacci(20));
    printf("Fibonacci(30) = %llu\n", fibonacci(30));
    printf("Fibonacci(40) = %llu\n", fibonacci(40));
}

// Recursive definition of function fibonacci
unsigned long long int fibonacci(int n) {
    if (0 == n || 1 == n) { // base case
        return n;
    }
    else { // recursive step
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}
```

```text
Fibonacci(0) = 0
Fibonacci(1) = 1
Fibonacci(2) = 1
Fibonacci(3) = 2
Fibonacci(4) = 3
Fibonacci(5) = 5
Fibonacci(6) = 8
Fibonacci(7) = 13
Fibonacci(8) = 21
Fibonacci(9) = 34
Fibonacci(10) = 55
Fibonacci(20) = 6765
Fibonacci(30) = 832040
Fibonacci(40) = 102334155
```

*Fig. 5.10* | Recursive fibonacci function.

The fibonacci calls from main are *not* recursive (lines 10 and 13–15), but all subsequent calls to fibonacci are recursive (line 24). Each time fibonacci is invoked, it immediately tests for the *base case*—n is equal to 0 or 1. If this is true, n is returned. Interestingly, if n is greater than 1, the recursion step generates *two* recursive calls, each a slightly simpler problem than the original call to fibonacci. The following diagram shows how function fibonacci would evaluate fibonacci(3):

![](img/43d318ad505997c339a3ea78d716d162_273_0.png)

### Order of Evaluation of Operands

This figure raises some interesting issues about the order in which C compilers will evaluate operators’ operands. This is a different issue from the order in which operators are applied to their operands—that is, the order dictated by the rules of operator precedence and grouping. The preceding diagram shows that while evaluating `fibonacci(3)`, two recursive calls will be made, namely `fibonacci(2)` and `fibonacci(1)`. But in what order will these calls be made? You might simply assume the operands will be evaluated left-to-right. For optimization reasons, C does not specify the order in which the operands of most operators (including `+`) are to be evaluated. Therefore, you should make no assumption about the order in which these calls will execute. The calls could execute `fibonacci(2)` first and then `fibonacci(1)`, or the calls could execute in the reverse order, `fibonacci(1)` then `fibonacci(2)`. In this and most other programs, the final result would be the same. But in some programs, the evaluation of an operand may have side effects that could affect the final result of the expression.

### Operators for which Operand Evaluation Order Is Specified

C specifies the operand evaluation order of only four operators—`&&`, `||`, the comma (`,`) operator and `?:`. The first three are binary operators whose operands are guaranteed to be evaluated left-to-right. [Note: The commas used to separate the arguments in a function call are not comma operators.] The last operator is C’s only ternary operator. Its leftmost operand is always evaluated first. If the leftmost operand evaluates to nonzero (true), the middle operand is evaluated next, and the last operand is ignored. If the leftmost operand evaluates to zero (false), the third operand is evaluated next, and the middle operand is ignored.

### Exponential Complexity

A word of caution is in order about recursive programs like the one we use here to generate Fibonacci numbers. Each level of recursion in the `fibonacci` function has a doubling effect on the number of calls. The number of recursive calls that execute to calculate the nth Fibonacci number is "on the order of 2ⁿ." This rapidly gets out of hand. Calculating only the 20th Fibonacci number would require on the order of 2²⁰ or about a million calls, calculating the 30th Fibonacci number would require on the order of 2^30 or about a billion calls, and so on. Computer scientists refer to this as exponential complexity. Problems of this nature can humble even the world's most powerful computers! Complexity issues in general, and exponential complexity in particular, are discussed in detail in the upper-level computer-science course generally called "Algorithms."

The example we showed in this section used an intuitively appealing solution to calculate Fibonacci numbers, but there are better approaches. Exercise 5.48 asks you to investigate recursion in more depth and propose alternate approaches to implementing the recursive Fibonacci algorithm.

### Self Check

1 (True/False) For optimization reasons, C specifies the order in which the operands of most operators (including +) are to be evaluated.

Answer: False. For optimization reasons, C does not specify the order in which the operands of most operators (including +) are to be evaluated. C specifies the order of evaluation of the operands of only four operators—&&, ||, the comma (,) operator and ?:.

2 (Multiple Choice) Consider the code in Fig. 5.10, which implements a recursive fibonacci function. Which of the following statements a), b) or c) is false?
a) All fibonacci calls in Fig. 5.10 are recursive calls.
b) Each time fibonacci is invoked, it immediately tests for the base case—n is equal to 0 or 1. If this is true, n is returned.
c) If n is greater than 1, the recursion step generates two recursive calls, each a slightly simpler problem than the original call to fibonacci.
d) All of the above statements are true.

Answer: a) is false. Actually, the calls to fibonacci from main are not recursive calls, but all subsequent calls to fibonacci are recursive (line 24).

## 5.16 Recursion vs. Iteration

In the previous sections, we studied two functions that can easily be implemented either recursively or iteratively. This section compares the two approaches and discusses why you might choose one approach over the other.

### Common Features of Iteration and Recursion

- Both iteration and recursion are based on a control statement: Iteration uses an iteration statement; recursion uses a selection statement.
- Both iteration and recursion involve repetition: Iteration uses an iteration statement; recursion achieves repetition through repeated function calls.
- Iteration and recursion each have a termination test: Iteration terminates when the loop-continuation condition fails; recursion when a base case is recognized.
- Counter-controlled iteration and recursion both gradually approach termination: Iteration keeps modifying a counter until the counter assumes a value
