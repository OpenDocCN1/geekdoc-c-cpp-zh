# 90

# C-SIMPLER

```
Enter the number of elements in the array.
n=5
enter the array values
10
20
30
40
50
Original array values:
10-->20-->30-->40-->50-->nAfter incrementing
```

Output 5.8 of Program 5.8

# 5.3. RECURSIVE FUNCTIONS

Refer to the Program 5.3 which is meant for calculating the factorial of a given number. The function factorial in the program makes use of 'iteration technique' to repeatedly calculate the value as follows.

```
for (i=1;i<=num;i++)
f=f*i;
```

Figure 5.4 Factorial using iteration

In each iteration, value of 'f' gets changed. When the termination condition is reached,(i.e.) when 'i greater than 'num', the loop stops. And the recently updated value in 'f' is returned as the answer. The same job can be done using a concept called 'recursion' where we don't need a loop for iteration. Before going to the programmatic solution, let's understand the concept of recursion theoretically.

Let's do some maths work with factorial program.
Formula for factorial is as follows,

```
factorial(n) = n * (n-1) * (n-2) * (n-3) * ****** 1
factorial(1)=factorial(0)=1
```

Examples,
factorial(2)=2*1=[similar to factorial(1)]
factorial(3)=3*2*1=[similar to factorial(2)]
factorial(4)=4*3*2*1=[similar to factorial(3)]

Our focus henceforth will be with the square bracket in the above examples.

As it observed , factorial finding problem can be broken down into parts of lower complexity.
(i.e.) factorial(5)=5*factorial(4);
factorial(4)=4*factorial(3);
factorial(3)=3*factorial(2);
factorial(2)=2*factorial(1);
factorial(1)=1*factorial(0);
So, factorial(5)=5*4*3*2*1*factorial(0)= 120

When we need to repeat an operation, we adopted iteration so far. Instead, when we call a function from itself each time with the value of variable changed, the process is called recursion So we learnt each the functions that called other functions and not themselves!!
Recursive functions -> Functions that call themselves
Program 5.9 explains the recursion concept.