
| Name | Value 1 | Value 2 |
|---|---|---|
| Greg Goldy | 1 | 75 |
| Peter Lamba | 4 | 23 |
| Sheila Bower | 3 | 55 |
| Mickey Miller | 4 | 67 |
| Peter Lamba | 1 | 23 |
| Danny Dillion | 3 | 89 |
| Mickey Miller | 3 | 89 |
| Peter Lamba | 1 | 67 |
| Danny Dillion | 2 | 37 |
| Sheila Bower | 4 | 89 |
| Mickey Miller | 2 | 78 |
| Lisa Fisher | 1 | 87 |
| Peter Lamba | 1 | 90 |
| Danny Dillion | 4 | 56 |

## QUICK REVIEW

- 1. The sequential search algorithm searches the list for a given item, starting with the first element in the list. It continues to compare the search item with the elements in the list until either the item is found or no more elements are left in the list with which it can be compared.
- 2. On average, the sequential search algorithm searches half of the list.
- 3. For a list of length \(n\), in a successful search, on average, the sequential search makes \(\frac{n+1}{2}=O(n)\) comparisons.
- 4. A sequential search is not efficient for large lists.
- 5. A binary search is much faster than a sequential search.
- 6. A binary search requires the list elements to be in order, that is, sorted.
- 7. To search for an item in a list of length 1024, a binary search requires no more than 11 iterations of the loop, and so no more than 22 comparisons.
- 8. For a list of length \(n\), in a successful search, on average, the binary search makes \(2\log_2 n - 3\) key comparisons.
- 9. Let \(f\) be a function of \(n\). By the term asymptotic, we mean the study of the function as \(n\) becomes larger and larger without bound.
- 10. Let \(f\) and \(g\) be real-valued functions. Assume that \(f\) and \(g\) are nonnegative, that is, for all real numbers \(n\), \(f(n)\ge 0\) and \(g(n)\ge 0\). We say that \(f(n)\) is Big-O of \(g(n)\), written \(f(n)=O(g(n))\), if there exist positive constants \(c\) and \(n_0\) such that \(f(n)\le c g(n)\) for all \(n\ge n_0\).
- 11. Let \(f(n)\) be a real-valued function such that \(f(n)=a_mn^m+a_{m-1}n^{m-1}+\cdots+a_1n+a_0\), where \(a_i\) are real numbers, \(a_m\ne 0\), \(n\ge 0\) and \(m\) is a nonnegative integer. Then \(f(n)=O(n^m)\).
- 12. Let \(L\) be a list of size \(n>1\). Suppose that the elements of \(L\) are sorted. If \(SRH(n)\) is the minimum number of comparisons needed, in the worst case, by using a comparison-based algorithm to recognize whether an element \(x\) is in \(L\), then \(SRH(n) \geq \log_2(n + 1)\).
- 13. The binary search algorithm is the optimal worst-case algorithm for solving search problems by using the comparison method.
- 14. To construct a search algorithm of the order less than \(\log_2 n\), it cannot be comparison based.
- 15. For a list of length \(n\), on average, bubble sort makes \(\frac{n(n-1)}{2}\) key comparisons and about \(\frac{n(n-1)}{4}\) item assignments.
- 16. The selection sort algorithm sorts a list by finding the smallest (or equivalently largest) element in the list and then moving it to the beginning (or end) of the list.
- 17. For a list of length \(n\), where \(n > 0\), the selection sort algorithm makes \(\frac{1}{2}n^2 - \frac{1}{2}n\) key comparisons and \(3(n-1)\) item assignments.
- 18. For a list of length \(n\), where \(n > 0\), on average, the insertion sort algorithm makes \(\frac{1}{4}n^2 + O(n)\) key comparisons and \(\frac{1}{4}n^2 + O(n)\) item assignments.
- 19. Let \(L\) be a list of \(n\) distinct elements. Any sorting algorithm that sorts \(L\) by comparison of the keys only, in its worst case, makes at least \(\Omega(n\log_2 n)\) key comparisons.
- 20. Both the quick sort and merge sort algorithms sort a list by partitioning it.
- 21. To partition a list, the quick sort algorithm first selects an item from the list called *pivot*. The algorithm then rearranges the elements so that the elements in one of the sublists are less than *pivot* and the elements in the other sublist are greater than or equal to *pivot*.
- 22. In a quick sort, the sorting work is done in partitioning the list.
- 23. On average, the number of key comparisons in a quick sort is \(O(n\log_2 n)\). In the worst case, the number of key comparisons in a quick sort is \(O(n^2)\).
- 24. The merge sort algorithm partitions the list by dividing it in the middle.
- 25. In a merge sort, the sorting work is done in merging the list.
- 26. The number of key comparisons in a merge sort is \(O(n\log_2 n)\).

## EXERCISES

The number in parentheses at the end of an exercise refers to the learning objective listed at the beginning of the chapter.

- 1. Mark the following statements as true or false.
  - a. The member that uniquely identifies a data item is called the key of that data item. (1)
  - b. A sequential search of a list assumes that the list elements are sorted in ascending order. (2)
  - c. A binary search of a list assumes that the list is sorted. (3)
  - d. A binary search is faster on ordered lists and slower on unordered lists. (3)
  - e. A binary search is faster on large lists, but a sequential search is faster on small lists. (2, 3)
  - f. For a sorted list of length 128, to determine whether an item is in the list, the binary search algorithm makes at most 16 comparisons. (3)
  - g. Let \(f(n) = n^4 - 8n^3 + 2\), where \(n\) is a nonnegative integer. Then \(f(n) = O(4n)\). (4)
  - h. Let \(n\) be a nonnegative integer. Then \(O(n) \leq O(n\log_2 n)\). (4)
  - i. For a list of length 100, the bubble sort given in this chapter makes exactly 4950 key comparisons to sort the list. (7)
  - j. For a list of length 100, the selection sort given in this chapter makes exactly 297 item assignments to sort the list. (8)
  - k. For a list of length 100, in the worst case the insertion sort given in this chapter makes exactly 5050 key comparisons to sort the list. (9)
  - l. Let \(L\) be a list of \(n\) distinct elements. Any sorting algorithm that sorts \(L\) by comparison of the keys only, in its worst case, makes at least \(\Omega(n\log_2 n)\) key comparisons. (10)
  - m. The quick sort algorithm partitions a list into two sublists such that the elements in the first sublist are less than *pivot* and the elements in the second sublist are greater than *pivot*. (11)
  - n. The merge sort algorithm partitions a list into two sublists such that the number of elements in the first sublist is less than the number of elements in the second sublist. (12)

- 2. Consider the following list:
  
  45, 78, 23, 12, 63, 90, 38, 56, 88, 15
  
  Using the sequential search as described in this chapter, how many comparisons are required to find whether the following item is in the list? (Recall that by comparisons we mean item comparisons, not index comparisons.) (2)
  
  - a. 90
  - b. 14
  - c. 45
  - d. 23
  - e. 5

- 3.
  - a. Write a version of the sequential search algorithm that can be used to search a sorted list. (1, 2)
  - b. Consider the following list:
    
    2, 20, 38, 41, 49, 56, 62, 70, 88, 95, 100, 135, 145
    
    Using a sequential search on ordered lists that you designed in (a), how many comparisons are required to determine whether the following items are in the list? (Recall that comparisons mean item comparisons, not index comparisons.) (1, 2)
    
    - i. 2
    - ii. 57
    - iii. 88
    - iv. 70
    - v. 135

- 4. Consider the following list:
  
  5, 12, 25, 32, 38, 46, 58, 62, 85, 90, 97, 105, 110
  
  Using the binary search as described in this chapter, how many comparisons are required to find whether the following items are in the list? Show the values of first, last, and middle and the number of comparisons after each iteration of the loop. (3)
  
  - a. 32
  - b. 20
  - c. 105
  - d. 60

- 5. Consider the following list:
  
  6, 25, 32, 39, 65, 77, 88, 99, 110, 124, 130
  
  Using the binary search, how many comparisons are required to determine whether the following items are in the list or not? (3)
  
  - a. 5
  - b. 25
  - c. 30
  - d. 65
  - e. 77
  - f. 110
  - g. 134

- 6. Suppose that L is a sorted list of 1024 elements. In a successful search, what is the maximum number of comparisons made by binary search to determine if an item is in L? (3)

- 7. Suppose that L is a sorted list of 4096 elements. What is the maximum number of comparisons made by binary search to determine if an item is in L? (3)

- 8. Each of the following expressions represents the number of operations for certain algorithms. What is the order of each of these expressions? (4)
  
  - a. n³ − 8n
  - b. 5n⁴ + 2n² + 8
  - c. (n² + n − 1)(8n + 5)
  - d. 8n(6n + 1)
  - e. 7(9 − 5m)

- 9. Let L be a sorted list of size 500. In the worst case, to determine whether an element x is in L, what is the minimum number of comparisons made by a comparison-based search algorithm? (5)

- 10. Sort the following list using the bubble sort algorithm as discussed in this chapter. Show the list after each iteration of the outer for loop. (7)
  
  50, 36, 78, 40, 4, 28, 90, 62, 22

- 11.
  - a. The number of comparisons in the best case of a bubble sort algorithm, as given in this chapter, is \(O(n^2)\). Show that the following version of the bubble sort algorithm reduces the number of comparisons in the best case of the bubble sort algorithm to \(O(n)\). (6)
