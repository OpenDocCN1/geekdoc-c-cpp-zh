| main() | Memory Snapshot |
| :--- | :--- |
| Step 1: int n;<br>Step 2: cin >> n;<br>Step 3: cout << ... << factorialR(n); | int n ?<br>int n 4 |
| factorialR(n) | |
| Step 4: return n*factorialR(3) | int n 4<br>stack *4*factorialR(3) |
| factorialR(3) | |
| Step 5: return 3*factorialR(2) | int n 3<br>stack 3*factorialR(2) |
| factorialR(2) | |
| Step 6: return 2*factorialR(1) | int n 2<br>stack 2*factorialR(1) |
| factorialR(1) | |
| Step 7: return n*factorialR(0) | int n 1<br>stack 1*factorialR(0) |
| factorialR(0) | |
| Step 8: return 1 | factorialR(0) returns 1<br>factorialR(1) returns 1*1<br>factorialR(2) returns 2*1<br>factorialR(3) returns 3*2<br>factorialR(4) returns 4*6 |

Figure 10.6 Program trace.

For large values of n, the value of n! can exceed even long integers. In these cases, the computations should be done using double values. An interesting approximation to n! is also discussed in the end-of-chapter problems.

A program trace of program chapter10_5 is provided in Figure 10.6.

# Fibonacci Sequence

A Fibonacci sequence is a sequence of numbers f0, f1, f2, f3, ..., in which the first two values (f0 and f1) are equal to 1, and each succeeding number is the sum of the previous two numbers. Thus, the first few values of the Fibonacci sequence are

1 1 2 3 5 8 13 21 34 ...