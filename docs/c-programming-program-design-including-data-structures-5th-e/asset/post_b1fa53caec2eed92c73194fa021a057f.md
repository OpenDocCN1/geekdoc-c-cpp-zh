
```cpp
template <class Type>
void unorderedLinkedList<Type>::recMergeSort(
                                      nodeType<Type>* &head)
{
    nodeType<Type>* otherHead;

    if (head != NULL)     //if the list is not empty
        if (head->link != NULL)    //if the list has more than
                                   //one node
        {
            divideList(head, otherHead);
            recMergeSort(head);
            recMergeSort(otherHead);
            head = mergeList(head, otherHead);
        }
} //end recMergeSort
```

We can now give the definition of the function `mergeSort`, which should be included as a public member of the class `unorderedLinkedList`. (Note that the functions `divideList`, `merge`, and `recMergeSort` can be included as private members of the class `unorderedLinkedList` because these functions are used only to implement the function `mergeSort`.) The function `mergeSort` calls the function `recMergeSort` and passes `first` to this function. It also sets `last` to point to the last node of the list. The definition of the function `mergeSort` is:

```cpp
template <class Type>
void unorderedLinkedList<Type>::mergeSort()
{
    recMergeSort(first);

    if (first == NULL)
        last = NULL;
    else
    {
        last = first;
        while (last->link != NULL)
            last = last->link;
    }
} //end mergeSort
```

We leave it as an exercise for you to write a program to test the merge sort algorithm. See Programming Exercise 13 at the end of this chapter.

## Analysis: Merge Sort

Suppose that $L$ is a list of $n$ elements, in which $n > 0$. Suppose that $n$ is a power of 2, that is, $n = 2^m$ for some nonnegative integer $m$, so that we can divide the list into two sublists, each of size:

$$\frac{n}{2} = \frac{2^m}{2} = 2^{m-1}$$

Moreover, each sublist can also be divided into two sublists of the same size. Each call to the function `recMergeSort` makes two recursive calls to the function `recMergeSort`, and each call divides the sublist into two sublists of the same size. Suppose that $m = 3$, that is, $n = 2^3 = 8$. So, the length of the original list is 8. The first call to the function `recMergeSort` divides the original list into two sublists, each of size 4. The first call then makes two recursive calls to the function `recMergeSort`. Each of these recursive calls divides each sublist, of size 4, into two sublists, each of size 2. We now have four sublists, each of size 2. The next set of recursive calls divides each sublist, of size 2, into sublists of size 1. So, we now have eight sublists, each of size 1. It follows that the exponent 3 in $2^3$ indicates the level of the recursion (see Figure 19-41).

![](img/f97f778697507bb6fdd80c5991210cba_1274_0.png)

Let us consider the general case when $n = 2^m$. Note that the number of recursion levels is $m$. Also, note that to merge a sorted list of size $s$ with a sorted list of size $t$, the maximum number of comparisons is $s + t - 1$.

Consider the function `mergeList`, which merges two sorted lists into a sorted list. Note that this is where the actual work (comparisons and assignments) is done. The initial call to the function `recMergeSort`, at level 0, produces two sublists, each of the size $n/2$. To merge these two lists, after they are sorted, the maximum number of comparisons is:

$$ n/2 + n/2 - 1 = n - 1 = O(n). $$

At level 1, we merge two sets of sorted lists, in which each sublist is of the size $n/4$. To merge two sorted sublists, each of the size $n/4$, we need, at most:

$$ n/4 + n/4 - 1 = n/2 - 1 $$

comparisons. Thus, at level 1 of the recursion, the number of comparisons is $2(n / 2 - 1) = n - 2 = O(n)$. In general, at level $k$ of the recursion, there are a total of $2^k$ calls to the function `mergeList`. Each of these calls merges two sublists, each of the size $n / 2^{k-1}$, which requires a maximum of $n / 2^k - 1$ comparisons. Thus, at level $k$ of the recursion, the maximum number of comparisons is:

$$2^k\left(\frac{n}{2^k}-1\right)=n-2^k=O(n).$$

It now follows that the maximum number of comparisons at each level of the recursion is $O(n)$. Because the number of levels of the recursion is $m$, the maximum number of comparisons made by the merge sort algorithm is $O(nm)$. Now $n = 2^m$ implies that $m = \log_2 n$. Hence, the maximum number of comparisons made by the merge sort algorithm is $O(n \log_2 n)$.

If $W(n)$ denotes the number of key comparisons in the worst case to sort $L$, then $W(n) = O(n \log_2 n)$.

Let $A(n)$ denote the number of key comparisons in the average case. In the average case, during merge, one of the sublists will exhaust before the other list. From this, it follows that, on average, when merging two sorted sublists of combined size $n$, the number of comparisons will be less than $n - 1$. On average, it can be shown that the number of comparisons for merge sort is given by the following equation: If $n$ is a power of 2, $A(n) = n \log_2 n - 1.25n = O(n \log_2 n)$. This is also a good approximation when $n$ is not a power of 2.

> **NOTE**
>
> We can also obtain an analysis of the merge sort algorithm by constructing and solving certain equations as follows. As noted before, in merge sort, all of the comparisons are made in the procedure `mergeList`, which merges two sorted sublists. If one sublist is of size $s$ and the other sublist is of size $t$, then merging these lists would require, at most, $s + t - 1$ comparisons in the worst case. Hence:
>
> $$W(n) = W(s) + W(t) + s + t - 1$$
>
> Note that $s = n / 2$ and $t = n / 2$. Suppose that $n = 2^m$. Then, $s = 2^{m-1}$ and $t = 2^{m-1}$. It follows that $s + t = n$. Hence:
>
> $$W(n) = W(n/2) + W(n/2) + n - 1 = 2W(n/2) + n - 1, \quad n > 0$$
>
> Also:
>
> $$W(1) = 0$$
>
> It is known that when $n$ is a power of 2, $W(n)$ is given by the following equation:
>
> $$W(n) = n \log_2 n - (n - 1) = O(n \log_2 n)$$

**(Heap Sort)** This chapter also discusses the heap sort algorithm. This algorithm and its related exercises are available at the Web site, *www.course.com/malik/cpp*, accompanying this book.

## PROGRAMMING EXAMPLE: Election Results

The presidential election for the student council of your local university is about to be held. The chair of the election committee wants to computerize the voting and has asked you to write a program to analyze the data and report the winner.

The university has four major divisions, and each division has several departments. For the election, the four divisions are labeled as region 1, region 2, region 3, and region 4. Each department in each division handles its own voting and reports the votes received by each candidate to the election committee. The voting is reported in the following form:

```
firstName lastName regionNumber numberOfVotes
```

The election committee wants the output in the following tabular form:

**Election Results**

| Candidate Name | Region1 | Region2 | Region3 | Region4 | Total |
|---|---:|---:|---:|---:|---:|
| Sheila Bower | 23 | 70 | 133 | 267 | 493 |
| Danny Dillion | 25 | 71 | 156 | 97 | 349 |
| Lisa Fisher | 110 | 158 | 0 | 0 | 268 |
| Greg Goldy | 75 | 34 | 134 | 0 | 243 |
| Peter Lamba | 285 | 56 | 0 | 46 | 387 |
| Mickey Miller | 112 | 141 | 156 | 67 | 476 |

Winner: Sheila Bower, Votes Received: 493

Total votes polled: 2216

The names of the candidates must be in alphabetical order in the output.

For this program, we assume that six candidates are seeking the student council’s president post. This program can be enhanced to handle any number of candidates.

The data are provided in two files. One file, *candData.txt*, consists of the names of the candidates seeking the president’s post. The names of the candidates in this file are in no particular order. In the second file, *voteDat.txt*, each line consists of the voting results in the following form:
