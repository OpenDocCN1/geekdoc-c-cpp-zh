```
0
6
9
2
1
Enter Search Element :6
Enter Element 6 Is Found At 5 Location
```

# ## 16.2.3 Fibonacci Search

The Fibonacci search is a technique of searching a sorted array using the divide and conquer principle that narrows down possible locations with the use of Fibonacci numbers. Compared to binary search, Fibonacci search finds the locations whose addresses have lower distribution. The advantage of Fibonacci search over binary search is that it slightly reduces the average time needed to access a storage location.

Fibonacci search has a complexity of O(log(n)). Instead of splitting the array in the middle, this implementation splits the array corresponding to the Fibonacci numbers, which are defined by the following recurrence relations:

```
F_0 = 0
F_1 = 1
F_n = 1
F_n = F_{n-1} + F_{n-2}, for n>=2
```

Fibonacci sequence when used as a search technique is termed as Fibonacci search. As the binary search determines the median in the new list as the next element for comparison, the Fibonacci search also determines the next element for comparison, which is indicated by the sequence of Fibonacci number. Fibonacci search performs search technique only on the ordered list. For the convenience of explanation, consider that the number of lists is one less than the Fibonacci number, i.e. n=F_{n-1}.

Consider an ancestor, parent and its child nodes to perform Fibonacci search on a decision tree that satisfies the following properties. If the difference in index between parent and ancestor is F_p, then

+   i. If the parent is a left child node, then the difference between parent and its child in an index is F_{p-1}.
+   ii. If the parent is a right child node, then the difference between parent and its child in the index is F_{p-2}.

Suppose consider an order list L = {E_1, E_2, E_3, ..., E_n}, where n is F_{k-1}. The Fibonacci search decision tree is shown in Figure 16.12. For n=20 where 20=F_{k-1}, the root of the decision tree which is the first element to be compared with the element ITEM is E_i, whose index i is the closest Fibonacci number to n. Here for n=20, 13 is the closest Fibonacci sequence number. So, E_i is the root.

If Item<E_i, then the next element to be compared is E_i. If Item>E_i, then the next element to be compared is E_a and so on. By the above properties, the other decision nodes can be easily determined. The right child of E_i should be E_a and for E_a the right child should be E_b, and so on.

Consider the nodes E_a and E_b and E_c, since E_a is the right child of E_b, the difference between them is 3, i.e. F_p (because F_p=F_{p-1}+F_3). The difference between E_a and its two children is F_q which is 1. Hence the two child nodes of E_a are E_a and E_b. Similarly consider the nodes E_a and E_b, is the left child of E_a and the difference between them is given by F_q, the two child nodes of E_a are given by E_a and E_b, their difference is F_q.

Algorithm 16.11 is the algorithm for Fibonacci search. Here DATA is an ordered list and n is the number of elements such that F_{k-1} > (n+1) and F_{k-2} = (n+1). Item is the one to be searched in the list.