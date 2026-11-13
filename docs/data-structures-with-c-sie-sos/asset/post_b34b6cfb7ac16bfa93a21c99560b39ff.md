
getch();
}

Output:
Enter the values of A, B and C: 1
-3
-4
X1= 4.00, X2= -1.00

## Iteration Logic (Repetitive Flow)

The third kind of logic refers to either of two types of structures involving loops. Each type begins with a Repeat statement and is followed by a module, called the *body of the loop*. For clarity, we will indicate the end of the structure by the statement [End of loop.] or some equivalent.

Each type of loop structure is discussed separately.

The *repeat-for loop* uses an index variable, such as K, to control the loop. The loop will usually have the form:

```
Repeat for K = R to S by T:
[Module]
[End of loop.]
```

The logic of this structure is pictured in Fig. 2.5(a). Here R is called the *initial value*, S the *end value* or *test value*, and T the *increment*. Observe that the body of the loop is executed first with K = R, then with K = R + T, then with K = R + 2T, and so on. The cycling ends when K > S. The flow chart assumes that the increment T is positive; if T is negative, so that K decreases in value, then the cycling ends when K < S.

![](img/f1df4c31f1795198a6843c842acc2216_43_0.png)

Fig. 2.5

The repeat-while loop uses a condition to control the loop. The loop will usually have the form Repeat while condition:
[Module]
[End of loop.]

The logic of this structure is pictured in Fig. 2.5(b). Observe that the cycling continues until the condition is false. We emphasize that there must be a statement before the structure that initializes the condition controlling the loop, and in order that the looping may eventually cease, there must be a statement in the body of the loop that changes the condition.

### Example 2.6

Algorithm 2.1 is rewritten using a repeat-while loop rather than a Go to statement:

- **Algorithm 2.3:** (Largest Element in Array) Given a nonempty array DATA with N numerical values, this algorithm finds the location LOC and the value MAX of the largest element of DATA.
- 1. [Initialize.] Set K := 1, LOC := 1 and MAX := DATA[1].
- 2. Repeat Steps 3 and 4 while K ≤ N:
- 3. If MAX < DATA[K], then:
-   Set LOC := K and MAX := DATA[K].
-   [End of If structure.]
- 4. Set K := K + 1.
-   [End of Step 2 loop.]
- 5. Write: LOC, MAX.
- 6. Exit.

### Program 2.3

```
/* C implementation of Algorithm 2.3*/
#include <stdio.h>
#include <conio.h>

void main()
{
int DATA[10]={22,65,1,99,32,17,74,49,33,2};
int N, LOC, MAX, K;
N=10;
K=0;
LOC=0;
MAX=DATA[0];
clrscr();

while(K<N)
{
if(MAX<DATA[K])
{
LOC=K;
MAX=DATA[K] ;
}
K=K+1;
}

printf("LOC= %d, MAX= %d",LOC,MAX) ;
getch();
}
```

Output:
LOC = 3, MAX= 99

Algorithm 2.3 indicates some other properties of our algorithms. Usually we will omit the word “Step.” We will try to use repeat structures instead of Go to statements. The repeat statement may explicitly indicate the steps that form the body of the loop. The “End of loop” statement may explicitly indicate the step where the loop begins. The modules contained in our logic structures will normally be indented for easier reading. This conforms to the usual format in structured programming.

Any other new notation or convention either will be self-explanatory or will be explained when it occurs.

## 2.5 COMPLEXITY OF ALGORITHMS

The analysis of algorithms is a major task in computer science. In order to compare algorithms, we must have some criteria to measure the efficiency of our algorithms. This section discusses this important topic.

Suppose M is an algorithm, and suppose n is the size of the input data. The time and space used by the algorithm M are the two main measures for the efficiency of M. The time is measured by counting the number of key operations—in sorting and searching algorithms, for example, the number of comparisons. That is because key operations are so defined that the time for the other operations is much less than or at most proportional to the time for the key operations. The space is measured by counting the maximum of memory needed by the algorithm.

The complexity of an algorithm M is the function f(n) which gives the running time and/or storage space requirement of the algorithm in terms of the size n of the input data. Frequently, the storage space required by an algorithm is simply a multiple of the data size n. Accordingly, unless otherwise stated or implied, the term “complexity” shall refer to the running time of the algorithm.

The following example illustrates that the function f(n), which gives the running time of an algorithm, depends not only on the size n of the input data but also on the particular data.

### Example 2.7

Suppose we are given an English short story TEXT, and suppose we want to search through TEXT for the first occurrence of a given 3-letter word W. If W is the 3-letter word “the,” then it is likely that W occurs near the beginning of TEXT, so f(n) will be small. On the other hand, if W is the 3-letter word “zoo,” then W may not appear in TEXT at all, so f(n) will be large.

The above discussion leads us to the question of finding the complexity function f(n) for certain cases. The two cases one usually investigates in complexity theory are as follows:

- 1. Worst case: the maximum value of f(n) for any possible input
- 2. Average case: the expected value of f(n)

Sometimes we also consider the minimum possible value of f(n), called the best case.

The analysis of the average case assumes a certain probabilistic distribution for the input data; one such assumption might be that all possible permutations of an input data set are equally likely. The average case also uses the following concept in probability theory. Suppose the numbers n1, n2, ..., nk occur with respective probabilities p1, p2, ..., pk. Then the expectation or average value E is given by

E = n1p1 + n2p2 + ... + nkpk

These ideas are illustrated in the following example.

### Example 2.8 Linear Search

Suppose a linear array DATA contains n elements, and suppose a specific ITEM of information is given. We want either to find the location LOC of ITEM in the array DATA, or to send some message, such as LOC = 0, to indicate that ITEM does not appear in DATA. The linear search algorithm solves this problem by comparing ITEM, one by one, with each element in DATA. That is, we compare ITEM with DATA[1], then DATA[2], and so on, until we find LOC such that ITEM = DATA[LOC]. A formal presentation of this algorithm follows.

- Algorithm 2.4: (Linear Search) A linear array DATA with N elements and a specific ITEM of information are given. This algorithm finds the location LOC of ITEM in the array DATA or sets LOC = 0.
- 1. [Initialize] Set K := 1 and LOC := 0.
- 2. Repeat Steps 3 and 4 while LOC = 0 and K ≤ N.
- 3. If ITEM = DATA[K], then: Set LOC := K.
- 4. Set K := K + 1. [Increments counter.]
- [End of Step 2 loop.]
- 5. [Successful?]
- If LOC = 0, then:
- Write: ITEM is not in the array DATA.
- Else:
- Write: LOC is the location of ITEM.
- [End of If structure.]
- 6. Exit.

### Program 2.4

```
/* C implementation of Algorithm 2.4*/
#include <stdio.h>
#include <conio.h>

void main()
{
int DATA[10]={22, 65, 1, 99, 32, 17, 74, 49, 33, 2};
int ITEM=17;
int N, LOC, K;
N=10;
K=0;
LOC=-1;
clrscr();
while(LOC==-1 && K<N)
{
 if(ITEM==DATA[K])
 LOC=K;
 K=K+1;
}
if(LOC==-1)
 printf("ITEM is not in the array DATA");
else
 printf("%d is the location of ITEM",LOC);
getch();
}
```

Output:
5 is the location of ITEM

The complexity of the search algorithm is given by the number C of comparisons between ITEM and DATA[K]. We seek C(n) for the worst case and the average case.

### Worst Case

Clearly the worst case occurs when ITEM is the last element in the array DATA or is not there at all. In either situation, we have

$C(n) = n$

Accordingly, C(n) = n is the worst-case complexity of the linear search algorithm.

### Average Case

Here we assume that ITEM does appear in DATA, and that it is equally likely to occur at any position in the array. Accordingly, the number of comparisons can be any of the numbers 1, 2, 3, ..., n, and each number occurs with probability p = 1/n. Then

$$C(n) = 1 \cdot \frac{1}{n} + 2 \cdot \frac{1}{n} + ... + n \cdot \frac{1}{n}
= (1 + 2 + ... + n) \cdot \frac{1}{n}
= \frac{n(n+1)}{2} \cdot \frac{1}{n} = \frac{n+1}{2}$$
