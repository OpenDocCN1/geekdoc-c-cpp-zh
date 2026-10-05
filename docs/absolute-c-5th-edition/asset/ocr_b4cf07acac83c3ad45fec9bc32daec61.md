# Programming Projects 609

do Programming Project 13.1 iteratively, rather than recursively; that is, the problem with a loop. You should compute Fibonacci number on the way to the number requested and discard the numbers when they are no longer needed.

+   b. Time the solution for Programming Project 13.1 and Part a of this project in finding the 1st, 3rd, 5th, 7th, 9th, 11th, 13th, and 15th Fibonacci numbers. Determine how long each function takes. Compare and comment on your results.

*Hints:* If you are running Linux, use the bash cime utility. It gives real time (in wall clock time), user time (measured by cpu cycles devoted to your program), and system time (cpu cycles devoted to tasks other than your). If you are running in some other environment, you will have to read your manual, or ask your instructor, in order to find out how measure the time a program takes to run.

+   7. You have first completed Programming Project 13.6 to work on this project When computing a Fibonacci number using the most straightforward recursive function definition, the recursive solution recomputes Fibonacci number many times. To compute $F_n = F_{n-1} + F_{n-2}$, it computes all the numbers in Fi a second time in computing by saving the numbers in array while computing $F_n$. Write another version of your recursive Fibonacci function based on this. In the recursive solution for calculating the Nth Fibonacci number, declare an array of size N. Array stores the $i$th (i≤N) Fibonacci number as it is computed the first time. Then use the array to avoid second (redundant) recalculation of the Fibonacci numbers. This time your solution as you do in Programming Project 13.6, and compare it to your results for the iterative solution.

+   8. A savings account typically accrues savings using compound interest. If you deposit $1000 with 10% interest rate per year, after one year you will have $1100. If you leave this money in the account for another year at 10% interest, you will have $1210. After three years you will have $1331, and so on.

Write a program that inputs the initial amount, an interest rate per year, and the number of years the money will accrue compound interest. Write a recursive function that calculates the amount of money that will be in the savings account using the input information.

To verify your function, the amount should equal $P(1+i)^n$, where $P$ is the amount initially saved, $i$ is the interest rate per year, and $n$ is the number of years.

+   9. We have n people in a room, where n is an integer greater than or equal to 1. Each person shakes hands with every other person. What is the total number, h(n), of handshakes? Write a recursive function to solve this problem. To get started, if there are only one or two people in the room,

```
handshake(1) = 0
handshake(2) = 1
```

If a third person enters the room, he or she must shake hands with each of the two people already there. This are two handshakes in addition to the number

![](bbox=[0.06, 0.765, 0.15, 0.85])