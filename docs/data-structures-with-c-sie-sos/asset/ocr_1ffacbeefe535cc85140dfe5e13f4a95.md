```
```c
int ITEM=17;
int N, LOC, K;
N=10;
K=0;
LOC=-1;
clrsrc();
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
}```
```

Output:
5 is the location of ITEM

The complexity of the search algorithm is given by the number C of comparisons between ITEM and DATA[K]. We seek C(n) for the worst case and the average case.

# Worst Case

Clearly the worst case occurs when ITEM is the last element in the array DATA or is not there at all. In either situation, we have

$C(n) = n$

Accordingly, C(n) = n is the worst-case complexity of the linear search algorithm.

# Average Case

Here we assume that ITEM does appear in DATA, and that it is equally likely to occur at any position in the array. Accordingly, the number of comparisons can be any of the numbers 1, 2, 3, ..., n, and each number occurs with probability p = 1/n. Then

$$C(n) = 1 \cdot \frac{1}{n} + 2 \cdot \frac{1}{n} + ... + n \cdot \frac{1}{n}
= (1 + 2 + ... + n) \cdot \frac{1}{n}
= \frac{n(n+1)}{2} \cdot \frac{1}{n} = \frac{n+1}{2}$$