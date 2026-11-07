
Figure 18-48 shows `candidateList` after adding the votes for each candidate—that is, after a call to the function `addVotes`.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1383_0.png)

**FIGURE 18-48** `candidateList` after a call to the function `addVotes`

## Print Heading and Print Results

To complete the program, we include a function to print the heading, which outputs the first four lines of the output. The following function accomplishes this task:

```cpp
void printHeading()
{
    cout << "       --------------------Election Results---------"
         << "----------" << endl << endl;
    cout << "                            Votes" << endl;
    cout << "       Candidate Name   Region1   Region2   Region3   "
         << "Region4   Total" << endl;
    cout << "       -----------   -------   -------   -------   "
         << "-------   -----" << endl;
}
```

We now describe the function `printResults`, which prints the results. Suppose that the variable `sumVotes` holds the total votes polled for the election, the variable `largestVotes` holds the largest number of votes received by a candidate, and the variable `winLoc` holds the index of the winning candidate in the array list. Further suppose that `temp` is an object of type `candidateType`. The algorithm for this function is:

- 1. Initialize `sumVotes`, `largestVotes`, and `winLoc` to zero.
- 2. For each candidate:
  - a. Retrieve the candidate’s data into `temp`.
  - b. Print the candidate’s name and relevant data.
  - c. Retrieve the total votes received by the candidate and update `sumVotes`.
  - d. `if (largestVotes < temp.getTotalVotes())`

    ```cpp
    {
        largestVotes = temp.getTotalVotes();
        winLoc = i;
    }
    ```
- 3. Output the final lines of output.

We leave the definition of the function `printResults` as an exercise. (See Programming Exercise 18.)

## PROGRAM LISTING (MAIN PROGRAM)

```cpp
//******************************************************************
// Author: D. S. Malik
//
// This program processes voting data for the student council
// president’s post. It outputs each candidate’s name and the
// votes they received. The name of the winner is also printed.
//******************************************************************

#include <iostream>
#include <string>
#include <fstream>
#include "candidateType.h"
#include "unorderedArrayListType.h"

using namespace std;

const int NO_OF_CANDIDATES = 6;

void fillNames(ifstream& inFile,
               unorderedArrayListType<candidateType>& cList);
void processVotes(ifstream& inFile,
                  unorderedArrayListType<candidateType>& cList);
void addVotes(unorderedArrayListType<candidateType>& cList);

void printHeading();
void printResults
             (const unorderedArrayListType<candidateType>& cList);

int main()
{
    unorderedArrayListType<candidateType>
                  candidateList(NO_OF_CANDIDATES);
    candidateType temp;

    ifstream inFile;

    inFile.open("candData.txt");
    if (!inFile)
    {
        cout << "Input file (candData.txt) does not exist. "
             << "Program terminates!!" << endl;
        return 1;
    }

    fillNames(inFile, candidateList);

    candidateList.sort();

    inFile.close();
    inFile.clear();

    inFile.open("voteData.txt");
    if (!inFile)
    {
        cout << "Input file (voteData.txt) does not exist. "
             << "Program terminates!!" << endl;
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
//the definition of the function printResults here.
```

**Sample Run:** After you have written the definitions of the functions of the class candidateType and of the function printResults and then run your program, it should produce the following output. (See Programming Exercise 18.)

### Election Results

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

## Input Files

```
candData.txt

Greg Goldy
Mickey Miller
Lisa Fisher
Peter Lamba
Danny Dillion
Sheila Bower
```

```
voteData.txt

Greg Goldy 2 34
Mickey Miller 1 56
Lisa Fisher 2 56
Peter Lamba 1 78
Danny Dillion 4 29
Sheila Bower 4 78
Mickey Miller 2 63
Lisa Fisher 1 23
Peter Lamba 2 56
Danny Dillion 1 25
Sheila Bower 2 70
Peter Lamba 4 23
Danny Dillion 4 12
Greg Goldy 3 134
Sheila Bower 4 100
Mickey Miller 3 67
Lisa Fisher 2 67
Danny Dillion 3 67
Sheila Bower 1 23
Mickey Miller 1 56
Lisa Fisher 2 35
Sheila Bower 3 78
Peter Lamba 1 27
Danny Dillion 2 34
Greg Goldy 1 75
Peter Lamba 4 23
Sheila Bower 3 55
Mickey Miller 4 67
Peter Lamba 1 23
Danny Dillion 3 89
Mickey Miller 3 89
Peter Lamba 1 67
Danny Dillion 2 37
Sheila Bower 4 89
Mickey Miller 2 78
Lisa Fisher 1 87
Peter Lamba 1 90
Danny Dillion 4 56
```

## QUICK REVIEW

- 1. The sequential search algorithm searches the list for a given item, starting with the first element in the list. It continues to compare the search item with the elements in the list until either the item is found or no more elements are left in the list with which it can be compared.
- 2. On average, the sequential search algorithm searches half of the list.
- 3. For a list of length $n$, in a successful search, on average, the sequential search makes $\frac{n+1}{2}=O(n)$ comparisons.
- 4. A sequential search is not efficient for large lists.
- 5. A binary search is much faster than a sequential search.
- 6. A binary search requires the list elements to be in order, that is, sorted.
- 7. To search for an item in a list of length 1024, a binary search requires no more than 11 iterations of the loop, and so no more than 22 comparisons.
- 8. For a list of length $n$, in a successful search, on average, the binary search makes $2\log_2 n-3$ key comparisons.
- 9. Let $f$ be a function of $n$. By the term asymptotic, we mean the study of the function $f$ as $n$ becomes larger and larger, without bound.
- 10. Let $f$ and $g$ be real-valued functions. Assume that $f$ and $g$ are nonnegative, that is, for all real numbers $n$, $f(n)\geq 0$ and $g(n)\geq 0$. We say that $f(n)$ is Big-O of $g(n)$, written $f(n)=O(g(n))$, if there exist positive constants $c$ and $n_0$ such that $f(n)\leq cg(n)$ for all $n\geq n_0$.
- 11. Let $f(n)$ be a nonnegative, real-valued function such that $f(n)=a_mn^m+a_{m-1}n^{m-1}+\cdots+a_1n+a_0$, wherein $a_i$ are real numbers, $a_m\neq 0$, $n\geq 0$, and $m$ is a nonnegative integer. Then, $f(n)=O(n^m)$.
- 12. Let \(L\) be a list of size \(n > 1\). Suppose that the elements of \(L\) are sorted. If \(SRH(n)\) is the minimum number of comparisons needed, in the worst case, by using a comparison-based algorithm to recognize whether an element \(x\) is in \(L\), then \(SRH(n) \geq \log_2(n+1)\).
- 13. The binary search algorithm is the optimal worst-case algorithm for solving search problems by using the comparison method.
- 14. To construct a search algorithm of the order less than \(\log_2 n\), it cannot be comparison based.
- 15. For a list of length \(n\), on average, the bubble sort algorithm makes \(\frac{n(n-1)}{2}\) key comparisons and about \(\frac{n(n-1)}{4}\) item assignments.
- 16. The selection sort algorithm sorts a list by finding the smallest (or equivalently largest) element in the list and then moving it to the beginning (or end) of the list.
- 17. For a list of length \(n\), in which \(n > 0\), the selection sort algorithm makes \(\frac{1}{2}n^2 - \frac{1}{2}n\) key comparisons and \(3(n-1)\) item assignments.
- 18. For a list of length \(n\), in which \(n > 0\), on average, the insertion sort algorithm makes \(\frac{1}{4}n^2 + O(n)\) key comparisons and \(\frac{1}{4}n^2 + O(n)\) item assignments.
- 19. Let \(L\) be a list of \(n\) distinct elements. Any sorting algorithm that sorts \(L\) by comparison of the keys only, in its worst case, makes at least \(\Omega(n\log_2 n)\) key comparisons.
- 20. Both the quick sort and merge sort algorithms sort a list by partitioning it.
- 21. To partition a list, the quick sort algorithm first selects an item from the list called pivot. The algorithm then rearranges the elements so that the elements in one of the sublists are less than pivot and the elements in the other sublist are greater than or equal to pivot.
- 22. In a quick sort, the sorting work is done in partitioning the list.
- 23. On average, the number of key comparisons in a quick sort is \(O(n\log_2 n)\). In the worst case, the number of key comparisons in a quick sort is \(O(n^2)\).
- 24. The merge sort algorithm partitions the list by dividing it in the middle.
- 25. In a merge sort, the sorting work is done in merging the list.
- 26. The number of key comparisons in a merge sort is \(O(n\log_2 n)\).

## EXERCISES

The number in parentheses at the end of an exercise refers to the learning objective listed at the beginning of the chapter.

- 1. Mark the following statements as true or false.
  - a. The member that uniquely identifies a data item is called the key of that data item. (1)
