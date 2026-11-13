
So, the instruction space occupied by the above program is 48 bytes.

In the disassembled program, the instructions of the main function started from 0 to 2f hexadecimal value.

So, the total memory occupied by the above main function is (30)16 = (48)10. Hence, the total instruction space is 48 bytes.

## 3.5.6 CALCULATING THE DATA SPACE

The data space is the total space occupied by the data, rodata, bss and heap sections of the executable program. So, let the space occupied by each of the said section is found. Because there is no dynamic memory allocation, the heap section will not be created at the runtime.

| Idx | Name | Size |
|---|---|---|
| 1. | .data | 00000000 |
| 2. | .bss | 00000000 |
| 3. | .rodata | 00000010 |

From the disassembled program object dump, Table 3.1 shows the size occupied by each of the program sections in hexadecimal.

## 3.5.7 SIZE OF DATA SECTION

This section holds all the initialized global variables. In the program, there are no initialized variables. So, the size will be zero. In Table 3.1, the first row shows the size occupied by the data section 00000000 is nothing but zero.

## 3.5.8 SIZE OF RODATA SECTION

Rodata section consists of constant values, because the section itself is a read-only section. In the above program, a constant is declared with 3.141. The constant value has taken 00000010 of hexadecimal or 16 bytes in decimal.

## 3.5.9 SIZE OF BSS SECTION

This section consists of uninitialized global data because there are no uninitialized variables. So, the size of the bss section should be zero. As shown in Table 3.1, the bss section taking 00000000 is nothing but zero.

So, the total data space is

Data space = size (data section) + size (rodata) + size (bss section)
Data space = 0 + 16 + 0 = 16 bytes

The total space complexity of the program is

Space complexity = Instruction space + data space + stack space
Space complexity = 48 + 16 + 0 = 64 bytes

So, the space complexity of the given program is 64 bytes.

### Example

```
#include<stdio.h>
#include<stdlib.h>
#define PI 3.141 */rodata*/
int a; /*bss section*/
int b=10; /*data section*/
static int c=20; /*data section*/
int main()
{
	char name[10] ;/*stack*/
	cout<<"\td \d"<<c<b;/*rodata*/
}
```

### Sections

| Idx | Name | Size | VMA | LMA | File off | Algn |
|---|---|---|---|---|---|---|
| 0 | .text | 0000003e | 00000000 | 00000000 | 00000034 | 2**2 |
| | | CONTENTS, ALLOC, LOAD, RELOC, READONLY, DATA | | | | |
| 1 | .data | 00000008 | 00000000 | 00000000 | 00000074 | 2**2 |
| | | CONTENTS, ALLOC, LOAD, DATA | | | | |
| 2 | .bss | 00000004 | 00000000 | 00000000 | 0000007c | 2**2 |
| | | CONTENTS, ALLOC, LOAD, DATA | | | | |
| 3 | .rodata | 00000006 | 00000000 | 00000000 | 0000007c | 2**0 |
| | | CONTENTS, ALLOC, LOAD, READONLY, DATA | | | | |

### Data space

size (data) + size (rodata) + size (bss) = 8 + 6 + 4 = 18 bytes

### Instruction space

(3e)16 = 62 bytes

### Stack space

4 Bytes Frame Pointer + 4 Bytes Stack Pointer + 12 Bytes of array = 20 bytes

Here the 10 bytes of array will be placed onto the word blocks of stack. When one word = 4 bytes, 10 bytes will be placed into 12 bytes (ie 3 words).
Space complexity = 18 + 62 + 20 = 100 bytes

## 3.6 APRIORI ANALYSIS

The empirical or theoretical approach may be used for computing the time complexities of algorithms.

In the empirical or posteriori testing approach, algorithms are completely implemented and are executed for various instances of the problem on a computer. The time taken to do this is considered and compared. Among the various algorithmic solutions, the algorithm that takes less time to implement it can be considered as the best one.

In the theoretical or apriori approach, the resources that are required by the algorithm are determined mathematically. When a problem is considered, the apriori approach is performed as a function of a parameter that is related to instances of the problem. The size of input instances is often used as a parameter. For different classes of problems there are algorithms that consider the number of basic operations or element comparisons or multiplications as a parameter in order to find out the efficiency.

Apriori analysis is totally machine, language and program independent. In apriori analysis, algorithm efficiency can be studied on any input instances of any size.

For a given program, a apriori analysis computes its efficiency by considering the frequency count of the statement as a function of the total frequency count of the statements in the program. Here, the frequency count is the number of times the statement is getting executed in the program.

Consider the statement c=a+b that is appearing in the following three program segments. The frequency count is estimated as

| Program Segment 1 | Frequency Count |
| :--- | :--- |
| . . . | . . . |
| c=a+b; | 1 |
| . . . | . . . |
| **Total Frequency Count is 1** | |

| Program Segment 2 | Frequency Count |
| :--- | :--- |
| . . . | . . . |
| for i=1 to n do | n+1 |
| c=a+b; | n |
| end | n |
| . . . | . . . |
| **Total Frequency Count is 3n+1** | |

| Program Segment 3 | Frequency Count |
| :--- | :--- |
| . . . | . . . |
| for j=1 to n do | n+1 |
| for i=1 to n do | \sum ... |
| c=a+b; | n^2 |
| end | \sum ... |
| **Total Frequency Count is 3n^2+3n+1** | |

In Program segment 1, the frequency count of the statement is 1. In Program segment 2 it is n as its for loop executes for n times. In Program segment 3 it is n^2 because it is embedded in a nested for loop where each of them are executed for n times.

In the three program segments, the total frequency counts are 1, (3n+1) and 3n^2+3n+1, respectively. The order of magnitude of the total frequency counts is proportional to 1, n and n^2. The notation O is explained in the Section 3.7.

## 3.7 ASYMPTOTIC NOTATION

Some of the algorithms may be short in the number of instructions but when input varies, the total number of execution steps grows gradually. The asymptotic notations will help to predict the program behavior at the runtime. It provides a measurable value. Using the asymptotic notations, the best algorithm can be found, which can perform better than the other possible algorithms of a problem. The asymptotic notations consider the operation count or step count of an algorithm.

### Example

Let A and B be the two algorithms for a problem where

```
A_n=3n^2+2n
B_n=5n
```

The computational growth of two algorithms varies with the n value as shown in Figure 3.1. In the graph, the x-axis represents the input variable values, i.e. n, and the y-axis represents the time complexity.

![](img/45784b9f0334626143002ec0d63692fd_121_0.png)

Figure 3.1 Computational growth changes

Algorithms A and B work similarly with respect to the time complexities when n=1.

- Time complexity of A=5 and
- Time complexity of B=5
- when n=2
- Time complexity of A=16 and
- Time complexity of B=10

Therefore, for n=2, B is the optimal algorithm.

Similar changes can be observed for other values of n as shown in the above graph.

## 3.7.1 Big oh Notation (O)

### Definition:

Let f(x) and g(x) be two non-negative functions defined on a set of real numbers. f(x) = O(g(x)) iff there exists positive constants ‘c’ and n0, such that f(n) <= cg(n) for all n >= n0,

The big oh notation considers the upper bound of the function.

### 3.7.1.1 Finding g(x), c and n0 Values

### Example 1

Let f(n) = 3n+2 for an algorithm. Computation of c, n0, and g(n) can be performed as f(n) = 3n+2. The function can be written in terms of g(n) as

```
f(n) <= c*g(n)
3n+2 <= c*g(n) because the function value is more than 3n, consider c=4, then
3n+2 <= 4*g(n) define g(x)=n
3n+2 <= 4n find n0.
Put n=1      3*1+2 <= 4*1 (condition failed)
So put n=2   3*2+2 <= 4*2 (true)
Put n=3      3*3+2 <= 4*3 (true)
Put n=4      3*4+2 <= 4*4 (true)
```

So, as per the mathematical induction, the function f(x) can be written in terms of g(x), and is true from n0=2 to all positive integers. The function f(x) can be defined as f(x)<=4n where n>=2

### Example 2

Let f(n) = 3n^4 + 2n^2 for an algorithm. Computation of c, n0, and g(n) can be performed as f(n) = 3n^4 + 2n^2

```
f(n) <= c*g(n) (Big oh notation)
3n^4 + 2n^2 <= c*g(n)
3n^4 + 2n^4 <= 4*g(n)
3n^4 + 2n^4 <= 4*g(n)   Let g(n) = n^4
3n^4 + 2n^4 <= 4*n^4
for n=1   5 <= 4*1 (Failed)
for n=2   56 <= 64 (True)
for n=3   261 <= 324 (True)
So, for all n>=2 f(x) = 3x^4 can be written as 4*n^4.
```

### 3.7.2 Omega Notation (Ω)

Definition: f(n) = Ω(g(n)) if there exists positive constants c and n0, such that f(n)>=c*g(n) for all n>=n0. In this case, the maximum possible lower bound will be selected.
