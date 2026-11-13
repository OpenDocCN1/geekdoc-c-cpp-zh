
For example

| f(x) | g(x) | |
|---|---|---|
| 10n^2 + 3n + 2 | n^2 | f(n) = O(n^2) |
| 4n + 2 | n | f(n) = O(n) |
| 5 | 1 | f(n) = O(1) |

## 3.7.2 Finding g(x), c, and n0 Values

### Example 1

Let f(n) = 3n + 2 for an algorithm. Computation of c, n0, and g(n) can be performed as f(n) = 3n + 2. The function can be written in terms of g(n) as

f(n) >= c*g(n)
3n + 2 >= c*g(n), let function value nearest minimum be 3n, consider c=3, then
3n + 2 >= 3*g(n) define g(x) = n
3n + 2 >= 3n find n0

- put n=1 ... 5 >= 3 (True)
- put n=2 ... 3*2+2 >= 3*2 (true)
- put n=3 ... 3*3+2 >= 3*3 (true)
- put n=4 ... 3*4+2 >= 3*4 (true)

So, as per the mathematical induction, the function f(x) can be written in terms of g(x), and is true for all n0 positive integers.

The function f(x) can be defined as f(x) >= 3n where n >= 1.

### Example 2

Let f(n) = 3n^4 + 2n^2 for an algorithm. Computation of c, n0, and g(n) can be performed as f(n) = 3n^4 + 2n^2.

f(n) >= c*g(n) (Omega notation)
3n^4 + 2n^2 >= c*g(n)
3n^4 + 2n^4 >= 3*g(n)
3n^4 + 2n^4 >= 3*g(n) Let g(n) = n^4
3n^4 + 2n^4 >= 3*n^4

- for n=1 ... 5 >= 3 (True)
- for n=2 ... 56 >= 48 (True)
- for n=3 ... 261 >= 243 (True)

So, for all n >= 1 function f(x) can be written as 3*n^4.

## 3.7.3 Theta Notation (θ)

**Definition:** f(n) = θ(g(n)) iff there exists positive constants c1 and c2 and n0 such that c1*g(n) <= f(n) <= c2*g(n) for all n >= n0,
In this notation, the value that lies in between the upper bound and maximum possible lower bounds will be selected.

### Example

| f(x) | g(x) |
|---|---|
| 10n^2 + 3n + 2 | n^2 |
| 4n+2 | n |

| f(n) | |
|---|---|
| f(n) = θ(n^2) | since f(n)>10n^2 and f(n) < 15n^2 for all n >= 1 |
| f(n) = θ(n) | since f(n)>4n and f(n) < 6n for all n >= 1 |

In the first example, f(x)=10n^2 + 3n + 2. The value of the function is always greater than g(x) = 10n^2 because some other expression and constant is available after the g(x) in the f(x). Consider n=1, in this case f(x) = 15 x 1 = 15. So, to find the upper bound for this function, it needs to consider multiples of 15, then g(x)=15n^2 will always greater than f(x).

In the second example, f(x) = 4n + 2. The value of the function is always greater than g(x) = 4n because some other expression and constant is available after g(x) in f(x). Consider n=1, in this case f(x) = 4 x 1 + 1 = 5. So, to find the upper bound for this function, it needs to consider multiples of 5, then g(x)=5n will always greater than f(x).

## 3.7.4 Little Oh Notation(o)

Definition: f(n)=o(g(n)) if f(n)=O(g(n)) and f(n)!=Ω(g(n)).

### Example

| f(n) | g(n) |
|---|---|
| 10n+2 | n^2 |

| f(n) | |
|---|---|
| f(n) = o(n^2) | since f(n) and f(n) != Ω(g(n)); however f(n) = O(n^2) |

## 3.8 TIME COMPLEXITY

Time complexity of a program can be defined as the total time taken for compilation and execution. The program has to be compiled before running it. Once the compilation process creates the executable binary file, to run the program, compilation is not required as long as there are no changes in the code. An executable binary file is required to run a program. Hence, consider only the execution time for calculating the time complexity.

The time complexity depends on the space complexity that the program uses, time taken to load the program, total number of executable instructions in the binary file, number of control loops present, number of function calls made, number of arithmetic operations used, number of console input/output operations, number of read/write locks and finally the input values of the program.

Consider a program to display natural numbers from 1 to n. If n=2, then the print function will be called only 2 times. If the n value is very high, then the print function will be called for n number of times.

If a program requires more memory than the available physical memory, then the processor makes use of virtual memory, which is placed in secondary storage devices such as a hard disk. Otherwise, the processor waits till sufficient physical memory is available. So, the runtime of a program depends on the space complexity. When the space complexity of the program is more than the available physical memory, then the runtime will be more. So, the time complexity of a simple program is very less than the complex huge program.

As the time complexity depends on so many factors, there is no exact procedure to find the time complexity of a program. But, by considering the basic operations and the number of times the operations are called, the time complexity can be estimated. The time complexity can be calculated by estimating the total number of instructions executed.

## 3.8.1 Time Complexity Analysis of Bubble Sort

### Program 3.1

```
//Program for Bubble Sort
#include<iostream.h>
#define MAX 256
void bubble(int a[], int n)
{
int i,j,temp;
//Start of Bubble Sort
for(i=0;i<n;i++)
{
for(j=0;j<(n-1);j++)
{
if(a[j]>a[j+1])
{
temp=a[j];
a[j]=a[j+1];
a[j+1]=temp;
}
}
}
// End of Bubble Sort
cout<<"\nSorted Array:";
for(i=0;i<n;i++)
{
cout<<"\n"<<a[i];
}
}
void main()
{
int i,n,a[256];
cout<<"\nEnter size:";
cin>>n;
for(i=0;i<n;i++)
{
cout<<"\nEnter Element:";
cin>>a[i];
}
bubble(a,n);
}
```

In Program 3.1, the bubble sort program accepts an array and size of the array as input arguments. The first for loop continues to execute for n times, the inner for loop executes for n-1 times and each time, three statements will be executed. So, the total number of executable statements in the program is n+(n-1)x3=3n²-3n. Therefore, time complexity of the program is O(n²).

## 3.8.2 TIME COMPLEXITY ANALYSIS OF SELECTION SORT

### Program 3.2

```
//Program for Selection Sort
#include<iostream.h>
//Function returns the maximum index of the array.
int maxindex(int a[], int n)
{
int i,temp,max_index=0;
for(i=1;i<n;i++)
{
if(a[max_index]<a[i])
{
max_index=i;
}
}
return(max_index);
}
void main()
{
int i,n,temp,a[256];
cout<<"\nEnter size :";
cin>>n;
for(i=0;i<n;i++)
{
cout<<"\nEnter Element :";
cin>>a[i];
}
/*Selection Sort Procedure*/
for(int s=n;s>1;s--)
{
int j=maxindex(a,s);
temp=a[j];
a[j]=a[s-1];
a[s-1]=temp;
}
/*Selection Sort Procedure*/
cout<<"\nSorted";
for(i=0;i<n;i++)
cout<<"\nElement :"<<a[i];
}
```

In Program 3.2, the maxindex function returns the index of the maximum number. In the worst case it runs for n times. The selection sort procedure has one loop, executes n times. For each n value, maxindex will be called and three statements of swapping procedure will be called for n times. Therefore, time complexity will be f(x)=n²+3n = O(n²).

## 3.9 WORST CASE, AVERAGE CASE AND BEST CASE COMPLEXITY

The number of steps an algorithm takes can be known when it is executed on the given input instance. To check the correctness of the algorithm, execute it for all instances. An algorithm when executed on all possible instances of data, the best, worst and average case complexities can be estimated. Suppose for the problem of sorting, the possible instances are the possible arrangements of all the possible keys. There is a need for differentiating at least three cases for which the efficiency of algorithm has to be determined.

### 3.9.1 Worst Case

The worst case complexity of an algorithm is when the algorithm takes maximum number of steps on any instance of size n. The Big oh notation tells the maximum upper bounds of the running time complexity. The Big oh time complexity can be called as worst case, because at any cost the maximum boundary will be O (Big oh) notation expression.

### 3.9.2 Average Case

The average case complexity of an algorithm is when the algorithm takes the average number of steps on any instance of size n. The Theta notation tells the time complexity that lies in between the maximum lower bounds and minimum upper bounds of the running time complexity. The Theta time complexity can be called as average case because at any cost the time complexity will not exceed Big O and Omega minimum boundary.

### 3.9.3 Best Case

The best case complexity of an algorithm is when the algorithm takes the minimum number of steps on any instance of size n. The Omega notation tells the time complexity, i.e., maximum possible lower bounds of the given function.

Consider the linear search performed on an unsorted array to find an element. If the element is found in the first cell then it is a best case. If the element is found in the last cell or not found in the array, then it is a worst case. In the worst case, all the elements will be checked. Then what is the average case? It is assumed that the chance of finding the element is equal all through the array. In this case, the probability that the element is found at the first cell is 1/n, the probability of finding the element in the second cell is 1/n and so on. Therefore, averaging all these probabilities gives the average number of steps taken to find the element. But, if the probability differs, then the average case complexity differs. The probability of finding an element in a particular cell has no effect on the best and worst cases.

## SUMMARY

- Algorithm is step-by-step process to solve a problem.
- The algorithms are the prior written steps to the implementation of software. The algorithm shows the clear path to get the required software solution.
- The segments of code used to represent an algorithm can be called as a pseudo code.
- Space complexity is the number of units of space the algorithm requires.
