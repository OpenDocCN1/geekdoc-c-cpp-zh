
```cpp
int main()
{
    unorderedArrayListType<candidateType> candidateList(NO_OF_CANDIDATES);
    candidateType temp;

    ifstream inFile;

    inFile.open("candData.txt");
    if (!inFile)
    {
        cout << "Input file (candData.txt) does not exist."
             << "Program terminates!!!" << endl;
        return 1;
    }

    fillNames(inFile, candidateList);

    candidateList.sort();

    inFile.close();
    inFile.clear();

    inFile.open("voteData.txt");
    if (!inFile)
    {
        cout << "Input file (voteData.txt) does not exist."
             << "Program terminates!!!" << endl;
        return 1;
    }

    processVotes(inFile, candidateList);
    addVotes(candidateList);

    printHeading();
    printResults(candidateList);

    return 0;
}
//Place the definitions of the functions fillNames,
//addVotes, processVotes, and printHeading here. Also, write and place
//the definitions of the function printResults here.
```

**Sample Run:** After you have written the definitions of the functions of the class `candidateType` and of the function `printResults` and then run your program, it should produce the following output. (See Program Listing Exercise 18.)

## Election Results

Votes

| Candidate Name | Region1 | Region2 | Region3 | Region4 | Total |
|---|---|---|---|---|---|
| Sheila Bower | 23 | 70 | 133 | 267 | 493 |
| Danny Dillon | 25 | 71 | 156 | 97 | 349 |
| Lisa Fisher | 110 | 158 | 0 | 0 | 268 |
| Greg Goldy | 75 | 34 | 134 | 0 | 243 |
| Peter Lamba | 285 | 56 | 0 | 46 | 387 |
| Mickey Miller | 112 | 141 | 156 | 67 | 476 |

Winner: Sheila Bower, Votes Received: 493

Total votes polled: 2216

### Input Files

**candData.txt**

- Greg Goldy
- Mickey Miller
- Lisa Fisher
- Peter Lamba
- Danny Dillon
- Sheila Bower

**voteData.txt**

- Greg Goldy 2 34
- Mickey Miller 1 56
- Lisa Fisher 2 56
- Peter Lamba 1 78
- Danny Dillon 4 29
- Sheila Bower 4 78
- Mickey Miller 2 63
- Lisa Fisher 1 23
- Peter Lamba 2 56
- Danny Dillon 1 25
- Sheila Bower 2 70
- Peter Lamba 4 23
- Danny Dillon 4 12
- Greg Goldy 3 134
- Sheila Bower 4 100
- Mickey Miller 3 67
- Lisa Fisher 2 67
- Danny Dillon 3 67
- Sheila Bower 1 23
- Mickey Miller 1 56
- Lisa Fisher 2 35
- Sheila Bower 3 78
- Peter Lamba 1 27
- Danny Dillon 2 34
- Greg Goldy 1 75
- Peter Lamba 4 23
- Sheila Bower 3 55
- Mickey Miller 4 67
- Peter Lamba 1 23
- Danny Dillon 3 89
- Mickey Miller 3 89
- Peter Lamba 1 67
- Danny Dillon 2 37
- Sheila Bower 4 89
- Mickey Miller 2 78
- Lisa Fisher 1 87
- Peter Lamba 1 90
- Danny Dillon 4 56

## QUICK REVIEW

- 1. The sequential search algorithm searches the list for a given item, starting with the first element in the list. It continues to compare the search item with the elements in the list until either the item is found or no more elements are left in the list with which it can be compared.
- 2. On average, the sequential search algorithm searches half of the list.
- 3. For a list of length $n$, in a successful search, on average, the sequential search makes $\frac{n+1}{2}=O(n)$ comparisons.
- 4. A sequential search is not efficient for large lists.
- 5. A binary search is much faster than a sequential search.
- 6. A binary search requires the list elements to be in order, that is, sorted.
- 7. To search for an item in a list of length 1024, a binary search requires no more than 11 iterations of the loop, and so no more than 22 comparisons.
- 8. For a list of length $n$, in a successful search, on average, the binary search makes $2\log_2 n-3$ key comparisons.
- 9. Let $f$ be a function of $n$. By the term asymptotic, we mean the study of the function $f$ as $n$ becomes larger and larger without bound.
- 10. Let $f$ and $g$ be real-valued functions. Assume that $f$ and $g$ are nonnegative, that is, for all real numbers $n$, $f(n)\ge 0$ and $g(n)\ge 0$. We say that $f(n)$ is Big-O of $g(n)$, written $f(n)=O(g(n))$, if there exist positive constants $c$ and $n_0$ such that $f(n)\le c g(n)$ for all $n\ge n_0$.
- 11. Let $f(n)$ be a nonnegative, real-valued function such that $f(n)=a_m n^m+a_{m-1}n^{m-1}+\cdots+a_1n+a_0$, wherein $a_i$ are real numbers, $a_m\ne 0$, $n\ge 0$, and $m$ is a nonnegative integer. Then, $f(n)=O(n^m)$.
- 12. Let L be a list of size n > 1. Suppose that the elements of L are sorted. If SRH(n) is the minimum number of comparisons needed, in the worst case, by using a comparison-based algorithm to recognize whether an element x is in L, then SRH(n) ≥ log₂(n + 1).
- 13. The binary search algorithm is the optimal worst-case algorithm for solving search problems by using the comparison method.
- 14. To construct a search algorithm of the order less than log₂ n, it cannot be comparison based.
- 15. For a list of length n, on average, the bubble sort algorithm makes n(n − 1)/2 key comparisons and about n(n − 1)/4 item assignments.
- 16. The selection sort algorithm sorts a list by finding the smallest (or equivalently largest) element in the list and then moving it to the beginning (or end) of the list.
- 17. For a list of length n, in which n > 0, the selection sort algorithm makes 1/2 n² − 1/2 n key comparisons and 3(n − 1) item assignments.
- 18. For a list of length n, in which n > 0, on average, the insertion sort algorithm makes 1/4 n² + O(n) key comparisons and 1/4 n² + O(n) item assignments.
- 19. Let L be a list of n distinct elements. Any sorting algorithm that sorts L by comparison of the keys only, in its worst case, makes at least Ω(n log₂ n) key comparisons.
- 20. Both the quick sort and merge sort algorithms sort a list by partitioning it.
- 21. To partition a list, the quick sort algorithm first selects an item from the list called pivot. The algorithm then rearranges the elements so that the elements in one of the sublists are less than pivot and the elements in the other sublist are greater than or equal to pivot.
- 22. In a quick sort, the sorting work is done in partitioning the list.
- 23. On average, the number of key comparisons in a quick sort is O(n log₂ n). In the worst case, the number of key comparisons in a quick sort is O(n²).
- 24. The merge sort algorithm partitions the list by dividing it in the middle.
- 25. In a merge sort, the sorting work is done in merging the list.
- 26. The number of key comparisons in a merge sort is O(n log₂ n).

## EXERCISES

- 1. Mark the following statements as true or false.
  - a. A sequential search of a list assumes that the list is in ascending order.
  - b. A binary search of a list assumes that the list is sorted.
  - c. A binary search is faster on ordered lists and slower on unordered lists.
  - d. A binary search is faster on large lists, but a sequential search is faster on small lists.

- 2. Consider the following list:

  35, 82, 45, 12, 56, 67, 92, 77

  Using the sequential search as described in this chapter, how many comparisons are required to find whether the following items are in the list? (Recall that by comparisons we mean item comparisons, not index comparisons.)

  - a. 12
  - b. 92
  - c. 65
  - d. 35

- 3.
  - a. Write a version of the sequential search algorithm that can be used to search a sorted list.
  - b. Consider the following list:

    8, 12, 15, 27, 35, 48, 65, 77, 86, 94, 120

    Using a sequential search on ordered lists, which you designed in (a), how many comparisons are required to determine whether the following items are in the list? (Recall that comparisons mean item comparisons, not index comparisons.)

    - i. 65
    - ii. 8
    - iii. 80
    - iv. 125

- 4. Consider the following list:

  5, 12, 25, 32, 38, 46, 58, 62, 85, 90, 97, 105, 110

  Using the binary search as described in this chapter, how many comparisons are required to find whether the following items are in the list? Show the values of first, last, and middle and the number of comparisons after each iteration of the loop.

  - a. 32
  - b. 20
  - c. 105
  - d. 60

- 5. Suppose that L is a sorted list of 4096 elements. What is the maximum number of comparisons made by the binary search algorithm, given in this chapter, to determine if an item is in L?

- 6. Sort the following list using the bubble sort algorithm as discussed in this chapter. Show the list after each iteration of the outer for loop.

  38, 60, 43, 57, 70, 58, 15, 10

- 7. a. The number of comparisons in the best case of a bubble sort algorithm, as given in this chapter, is O(n²). Show that the following version of the bubble sort algorithm reduces the number of comparisons in the best case of the bubble sort algorithm to O(n).
