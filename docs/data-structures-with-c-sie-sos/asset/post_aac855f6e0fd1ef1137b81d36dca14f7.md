
Observe that the first row contains the six permutations beginning with 1, the second row those beginning with 2, and so on.

## 2.4 Find: (a) \(2^{-5}, 8^{2/3}, 25^{-3/2}\); (b) \(\log_2 32, \log_{10} 1000, \log_2 (1/16)\); (c) \(\lfloor \log_2 1000 \rfloor, \lfloor \log_2 0.01 \rfloor\).

(a) \(2^{-5} = 1/2^5 = 1/32\); \(8^{2/3} = (\sqrt[3]{8})^2 = 2^2 = 4\); \(25^{-3/2} = 1/25^{3/2} = 1/5^3 = 1/125\).

(b) \(\log_2 32 = 5\) since \(2^5 = 32\); \(\log_{10} 1000 = 3\) since \(10^3 = 1000\); \(\log_2(1/16) = -4\) since \(2^{-4} = 1/2^4 = 1/16\).

(c) \(\lfloor \log_2 1000 \rfloor = 9\) since \(2^9 = 512\) but \(2^{10} = 1024\); \(\lfloor \log_2 0.01 \rfloor = -7\) since \(2^{-7} = 1/128 < 0.01 < 2^{-6} = 1/64\).

## 2.5 Plot the graphs of the exponential function \(f(x) = 2^x\), the logarithmic function \(g(x) = \log_2 x\) and the linear function \(h(x) = x\) on the same coordinate axis. (a) Describe a geometric property of the graphs \(f(x)\) and \(g(x)\). (b) For any positive number \(c\), how are \(f(c)\), \(g(c)\) and \(h(c)\) related?

Figure 2.8 pictures the three functions.

![](img/f1df4c31f1795198a6843c842acc2216_56_0.png)

Fig. 2.8

(a) Since \(f(x) = 2^x\) and \(g(x) = \log_2 x\) are inverse functions, they are symmetric with respect to the line \(y = x\).

(b) For any positive number \(c\), we have:

\(g(c) < h(c) < f(c)\)

In fact, as \(c\) increases in value, the vertical distances between the functions, \(h(c) - g(c)\) and \(f(c) - h(c)\), increase in value. Moreover, the logarithmic function \(g(x)\) grows very slowly compared with the linear function \(h(x)\), and the exponential function \(f(x)\) grows very quickly compared with \(h(x)\).

## Algorithms, Complexity

## 2.6 Consider Algorithm 2.3, which finds the location LOC and the value MAX of the largest element in an array DATA with n elements. Consider the complexity function C(n), which measures the number of times LOC and MAX are updated in Step 3. (The number of comparisons is independent of the order of the elements in DATA.)
(a) Describe and find C(n) for the worst case.
(b) Describe and find C(n) for the best case.
(c) Find C(n) for the average case when n = 3, assuming all arrangements of the elements in DATA are equally likely.

(a) The worst case occurs when the elements of DATA are in increasing order, where each comparison of MAX with DATA[K] forces LOC and MAX to be updated. In this case, C(n) = n - 1.

(b) The best case occurs when the largest element appears first and so when the comparison of MAX with DATA[K] never forces LOC and MAX to be updated. Accordingly, in this case, C(n) = 0.

(c) Let 1, 2 and 3 denote, respectively, the largest, second largest and smallest elements of DATA. There are six possible ways the elements can appear in DATA, which correspond to the 3! = 6 permutations of 1, 2, 3. For each permutation p, let np denote the number of times LOC and MAX are updated when the algorithm is executed with input p. The six permutations p and the corresponding values np follow:

| Permutation p: | 123 | 132 | 213 | 231 | 312 | 321 |
| Value of np: | 0 | 0 | 1 | 1 | 1 | 2 |

Assuming all permutations p are equally likely,

```
C(3) = \frac{0 + 0 + 1 + 1 + 1 + 2}{6} = \frac{5}{6}
```

(The evaluation of the average value of C(n) for arbitrary n lies beyond the scope of this text. One purpose of this problem is to illustrate the difficulty that may occur in finding the complexity of the average case of an algorithm.)

## 2.7 Suppose Module A requires M units of time to be executed, where M is a constant. Find the complexity C(n) of each algorithm, where n is the size of the input data and b is a positive integer greater than 1.

### (a) Algorithm P2.7A:

1. Repeat for I = 1 to N:
2. Repeat for J = 1 to N:
3. Repeat for K = I to N:
4. Module A.

[End of Step 3 loop.]
[End of Step 2 loop.]
[End of Step 1 loop.]
5. Exit.

### (b) Algorithm P2.7B:

1. Set J := 1.
2. Repeat Steps 3 and 4 while J <= N:
3. Module A.
4. Set J := B x J.
[End of Step 2 loop.]
5. Exit.

Observe that the algorithms use N for n and B for b.

(a) Here \( C(n) = \sum_{i=1}^n \sum_{j=1}^n \sum_{k=1}^n M \)

The number of times \( M \) occurs in the sum is equal to the number of triplets \( (i, j, k) \), where \( i, j, k \) are integers from 1 to \( n \) inclusive. There are \( n^3 \) such triplets. Hence

\( C(n) = Mn^3 = O(n^3) \)

(b) Observe that the values of the loop index J are the powers of \( b \):

\( 1, b, b^2, b^3, b^4, ... \)

Therefore, Module A will be repeated exactly \( T \) times, where \( T \) is the first exponent such that

\( b^T > n \)

Hence, \( T = \lfloor \log_b n \rfloor + 1 \)

Accordingly, \( C(n) = MT = O(\log_b n) \)

## 2.8 (a) Write a procedure FIND(DATA, N, LOC1, LOC2) which finds the location LOC1 of the largest element and the location LOC2 of the second largest element in an array DATA with \( n > 1 \) elements.

(b) Why not let FIND also find the values of the largest and second largest elements?

(a) The elements of DATA are examined one by one. During the execution of the procedure, FIRST and SECOND will denote, respectively, the values of the largest and second largest elements that have already been examined. Each new element DATA[K] is tested as follows. If

SECOND <= FIRST < DATA[K]

then FIRST becomes the new SECOND element and DATA[K] becomes the new FIRST element. On the other hand, if

SECOND < DATA[K] <= FIRST

then DATA[K] becomes the new SECOND element. Initially, set FIRST := DATA[1] and SECOND := DATA[2], and check whether or not they are in the right order. A formal presentation of the procedure follows:

### Procedure P2.8: FIND(DATA, N, LOC1, LOC2)

1. Set FIRST := DATA[1], SECOND := DATA[2], LOC1 := 1, LOC2 := 2.
2. [Are FIRST and SECOND initially correct?]
If FIRST < SECOND, then:
(a) Interchange FIRST and SECOND,
(b) Set LOC1 := 2 and LOC2 := 1.
[End of If structure.]
3. Repeat for K = 3 to N:
If FIRST < DATA[K], then:
(a) Set SECOND := FIRST and FIRST := DATA[K].
(b) Set LOC2 := LOC1 and LOC1 := K.
Else if SECOND < DATA[K], then:
Set SECOND := DATA[K] and LOC2 := K.
[End of If structure.]
[End of loop.]
4. Return.

(b) Using additional parameters FIRST and SECOND would be redundant, since LOC1 and LOC2 automatically tell the calling program that DATA[LOC1] and DATA[LOC2] are, respectively, the values of the largest and second largest elements of DATA.

### Program 2.8

```c
/* C implementation of Procedure P 2.8 */
#include <stdio.h>
#include <conio.h>

int DATA[10]={22,65,1,99,32,17,74,49,33,2};
int N, LOC1, LOC2, FIRST, SECOND;

void main()
{
void FIND(int [],int,int,int);
clrscr();
N=10;
LOC1=-1;
LOC2=-1;

FIND(DATA,N,LOC1,LOC2);
printf("FIRST = %d, LOC1 = %d, SECOND = %d, LOC2 = %d",FIRST,LOC1,SECOND,
LOC2);
getch();
}

void FIND(int LIST[],int LEN,int L1,int L2)
{
int TEMP,K;
FIRST=LIST[0];
SECOND=LIST[1];
L1=0;
L2=1;
if(FIRST<SECOND)
{
TEMP=FIRST;
FIRST=SECOND;
SECOND=TEMP;
L2=0;
L1=1;
}
for(K=2;K<LEN;K++)
{
if(FIRST<LIST[K])
{
SECOND=FIRST;
FIRST=LIST[K];
L2=L1;
L1=K;
}
else if(SECOND<LIST[K])
{
SECOND=LIST[K];
L2=K;
}
}
LOC1=L1;
LOC2=L2;
}
```

Output:
FIRST = 99, LOC1 = 3, SECOND = 74, LOC2 = 6

## 2.9 An integer $n > 1$ is called a *prime* number if its only positive divisors are 1 and $n$; otherwise, $n$ is called a *composite* number. For example, the following are the prime numbers less than 20:

2, 3, 5, 7, 11, 13, 17, 19

If $n > 1$ is not prime, i.e., if $n$ is composite, then $n$ must have a divisor $k \neq 1$ such that $k \le \sqrt{n}$ or, in other words, $k^2 \le n$.

Suppose we want to find all the prime numbers less than a given number $m$, such as 30. This can be done by the “sieve method,” which consists of the following steps. First list the 30 numbers:

1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15
16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30

Cross out 1 and the multiples of 2 from the list as follows:

1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15
16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30

Since 3 is the first number following 2 that has not been eliminated, cross out the multiples of 3 from the list as follows:

1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15
16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30

Since 5 is the first number following 3 that has not been eliminated, cross out the multiples of 5 from the list as follows:

1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15
16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30

Now 7 is the first number following 5 that has not been eliminated, but $7^2 > 30$. This means the algorithm is finished and the numbers left in the list are the primes less than 30:

2, 3, 5, 7, 11, 13, 17, 19, 23, 29

Translate the sieve method into an algorithm to find all prime numbers less than a given number $n$.

First define an array A such that

A[1] = 1, A[2] = 2, A[3] = 3, A[4] = 4, ..., A[N - 1] = N - 1, A[N] = N

We cross out an integer L from the list by assigning A[L] = 1. The following procedure CROSSOUT tests whether A[K] = 1, and if not, it sets

A[2K] = 1, A[3K] = 1, A[4K] = 1, ...

That is, it eliminates the multiples of K from the list
