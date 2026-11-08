
- 27.
  ```cpp
  template <class Type>
  int queueType<Type>::queueCount()
  {
      return count;
  }
  ```
- 29. The answer to this question is available at the Web site accompanying this book.
- 31. The answer to this question is available at the Web site accompanying this book.

## Chapter 18

- 1. a. false; b. true; c. false; d. false
- 3.
  - a.
    ```cpp
    template <class elemType>
    int seqOrdSearch(const elemType list[], int length,
                     const elemType& item)
    {
        int loc;
        bool found = false;

        for (loc = 0; loc < length; loc++)
            if (list[loc] >= item)
            {
                found = true;
                break;
            }

        if (found)
            if (list[loc] == item)
                return loc;
            else
                return -1;
        else
            return -1;
    } //end seqOrdSearch
    ```
  - b. i. 8  ii. 2  iii. 10  iv. 11
- 5. 26
- 7.
  - a. Suppose that the list is of length n. Then length = n. Consider the first iteration of the outer for loop, that is, when the value of iteration = 1. Now the inner loop executes n − 1 time. Before the execution of the inner for loop, the variable isSorted is set to true, assuming that the list is sorted. If the list is already sorted, then the expression list[index] > list[index + 1] in the if statement always evaluates to false, so the body of the if statement never executes. Because the inner loop executes n − 1 times, there are n − 1 comparisons. In the second iteration of the outer loop, because the variable isSorted is true, the loop condition, (iteration < length) && !isSorted, evaluates to false, so the outer for loop terminates. It follows that, if the list is already sorted, the outer for loop executes only once. Hence, the total number of comparisons is n − 1 = O(n).
  - b. 30
  - c. 3
- 11. 4, 15, 18, 20, 25, 32, 45, 91, 62, 88, 66
- 13. In quick sort, the list is partitioned according to an element, called pivot, of the list. After partitioning, elements in the first sublist are smaller than the pivot and in the second sublist are larger than the pivot. The merge sort partitions the list by dividing it into two sublists of nearly equal size by breaking the list in the middle.
- 15.
  - a. 9, 2, 13, 36, 55, 23, 62, 95, 86, 65, 75, 74, 89, 100, 98
  - b. 6
  - c. 2 and 3
- 17.
  - a. 48
  - b. 22, 30, 9, 15, 25, 18, 3, 48, 66, 95, 94, 55, 80, 50, 62
  - c. 15
  - d. 7 and 7
- 19. The function partition is called 9 times and the number of comparisons to sort the list is 37.
- 21. Quick sort: 10000 × log₂(10000) = 132878; merge sort: 132878.

## Chapter 19

- 1. a. false; b. true; c. false; d. false
- 3. L₄ = {B, D, E, H, I, K, L, M}
- 5. L₃ = {D, H, K}
- 7. L₂ = {I, L, M}
- 9. 3
- 11. 2
- 13. 2
- 15. A, B, E, I, and L
- 17. A, B, D, H, K, E, I, L, M, C, F, J, G
- 19. 68~95~75~80~85~90
- 21. Binary search tree after deleting 60.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1639_0.png)

- 23. Delete node 75 and redraw the binary tree.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1639_1.png)

- 25. Each node has two pointers. Thus, there are 2n pointers in all the nodes of the binary tree. The pointer pointing to the root node is an external pointer. Each of the remaining n − 1 nodes has one pointer pointing to it, which is a pointer from the parent node. The remaining pointers in all the nodes, which is 2n − (n − 1) = n + 1, are NULL. This implies that the binary tree has n + 1 empty subtrees.
- 27.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1640_0.png)

- 29.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1640_1.png)

- 31. The answer to this question is available at the Web site accompanying this book.

## Chapter 20

- 1. 0-3-4-7-10
- 3. This graph is simple.
- 5. Vertices 2 and 4 are not connected. So there is no path from vertex 2 to vertex 4.
- 7. 0-2-6-10-11
- 9. $\begin{bmatrix}0&1&1&0&0&0\\0&0&0&0&0&0\\0&1&0&1&0&0\\0&0&0&0&0&0\\0&0&2&0&0&0\\0&1&0&1&1&0\end{bmatrix}$
- 11. 0, 2, 1, 3, 4, 5
- 13. 0, 1, 2, 6, 7, 3, 11, 4, 5, 8, 10, 9
- 15. $\begin{bmatrix}\infty&10&6&\infty&\infty&\infty&\infty\\\infty&\infty&\infty&\infty&\infty&\infty&\infty\\\infty&\infty&\infty&\infty&\infty&4&8\\3&\infty&\infty&\infty&11&\infty&\infty\\\infty&\infty&\infty&\infty&\infty&\infty&\infty\\\infty&6&\infty&\infty&\infty&\infty&10\\\infty&\infty&\infty&\infty&\infty&\infty&\infty\end{bmatrix}$
- 17.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1641_0.png)

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1642_0.png)

Source Vertex: 0

| Edges | Weight |
| --- | --- |
| (3, 1) | 3 |
| (1, 2) | 2 |
| (6, 3) | 2 |
| (0, 4) | 3 |
| (2, 5) | 1 |
| (4, 6) | 3 |
| (5, 7) | 5 |

A minimal spanning tree weight: 19

## Chapter 21

- 1. The three main components of the STL are: containers, iterators, and algorithms.
- 3. A container is used to store data, while an algorithm is used to manipulate the data stored in a container.
- 5. An STL function object contains a function that can be treated as a function using the function call operator.
- 7. `vecList = {35, 67, 35, 67, 87, 10, 92, 11, 17, 82, 5, 15}`
- 9.
  - a. `intList1 = {7, 8, 19, 90, 15, 13, 15, 16, 18, 90, 30, 11, 88, 26}`
  - b. `intList1 = {12, 14, 20, 13, 15, 16, 18, 90, 30, 11, 88, 26}`
- 11. A `back_inserter` uses the `push_back` operation of the container, while a `front_inserter` uses the `push_front` operation of the container to add elements to the container. Furthermore, a `front_inserter` cannot be used for the vector container.
- 13. 5
- 15. a b c * e ¤ f § h 8
- 17. 5 56 27 2 78 30 35 48 36
- 19. 9

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1644_0.png)

## INDEX

Note: Page numbers in boldface indicate key terms.

- & (ampersand), 364, 365, 372, 518
- <> (angle brackets), 30, 35
- * (asterisk), 7, 37, 78
- \\ (backslash), 535
- , (comma), 35, 40, 90
- {} (curly braces), 7, 83, 90, 203, 214, 220, 398, 592, 726
- " (double quotes), 30, 78, 476
- = (equal sign), 35, 59, 161
- ! (exclamation point), 35
- / (forward slash), 31, 35, 159
- - (hyphen), 35
- () (parentheses), 46, 195, 199, 288, 1341
- . (period), 35, 594, 635
- + (plus sign), 40, 634
- # (pound sign), 10, 79, 634, 1162
- ? (question mark), 35
- ; (semicolon), 35, 77, 87, 90, 199, 201, 211, 263, 290, 593, 631
- ~ (tilde), 657
- _ (underscore), 36, 37, 55, 471
- **@**
- abacus, 2
- abs function, 337, 342
- abstract classes
  - binary trees and, 1320
  - described, **827**
  - linked lists and, 1045, 1049–1051
  - pure virtual functions and, 826–834
- abstract data types. See ADTs (abstract data types); data abstraction
- access functions, **644**, 645–647
- acos function, 1552
- action statements, **197**, 205
- actual parameters, **342**. See also parameters
- accumulate function, 1448, 1501–1506
- Ada, 744
- addFirst function, 384
- addition (+) operator, 43, 45, 46–49
- addQueue function, 1174, 1176–1179, 1183, 1187–1188, 1190, 1204–1205
- address (&) operator
  - classes and, 848–850
  - described, 783
  - overview, 783–784
  - pointers and, 783–784
- addresses, of memory cells, 4, 5, 33
- addressOfX function, 849
- addVotes function, 1291
- adjacency lists, 1367
- adjacency matrix, 1366
- adjacent from, use of the term, 1365
- adjacent to, use of the term, 1365
- adjacent vertices, 1365
- adjacent_difference function, 1448, 1501–1506
- adjacent_find function, 1446, 1452, 1479–1483
- ADTs (abstract data types)
  - binary trees and, 1317, 1327
  - described, 658
  - grade report program and, 747–748, 751
  - graphs and, 1368–1371, 1388
  - lists and, 836–838, 847, 1036, 1045–1057, 1066–1077, 1080–1081
  - overview, 658–660
  - queues and, 1173–1174, 1176, 1193, 1196–1198, 1200–1201, 1204–1205
  - stacks and, 1126–1127
  - structs and, 661
  - templates and, 935
- age variable, 139, 140, 141
- aggregate operations, 517
- aggregation. See composition
- Aiken, Howard, 3
- airline seating program, 589
- algebra, 336–337
- algorithm(s),
  - ANSI/ISO Standard C++ and, 22
  - arrays and, 514
  - cable company billing program and, 234, 236
  - change calculations and, 99–102
  - charitable donations program and, 162
  - classifications, 1446–1448
  - classifying numbers and, 295–297, 403–406
  - code detection program and, 559–562
  - control structures and, 207, 234, 236, 295–297, 301–302
  - data comparison program and, 409–410, 412–413
  - described, 12
  - divisibility tests and, 301–302
  - functions and, 356, 359
  - generic, 1446
  - grade report program and, 747–748
  - heap, 1448
  - juice machine program and, 679–680
  - largest number program and, 362
  - length calculations and, 96–99
  - modifying, 1447
  - non-modifying, 1446
  - overview, 21
  - problem-analysis-coding-execution cycle and, 12–20
  - rock, paper, and scissors game and, 463, 468–469
  - sales data analysis and, 609–611, 617–618
  - search, 526–535
  - sort, 530, 531–535
  - stacks and, 1143–1144
  - STL and, 1400, 1445–1506
  - strings and, 490–491, 493–494
  - student grade program and, 167–170
  - text processing program and, 565–566, 568
- algorithm header file, 1445, 1446, 1456, 1460, 1472, 1484
- American Standard Code for Information Interchange. See ASCII (American Standard Code for Information Interchange)
- amount due variable, 57
- ampersand (&), 364, 365, 372, 518
- analog signals, 6
- and (&&) operator, 190–195, 208, 313
- angle brackets (< >), 30, 35
- anonymous data types, 461
- ANSI (American National Standards Institute), 22
- ANSI/ISO Standard C++. See also Standard C++
  - namespaces and, 81, 471, 472
  - naming conventions, 1544–1545
  - overview, 22
  - string data types and, 53, 476, 555
- append function, 480
- application programs, 6
- area function, 717, 719, 724, 725, 873
- area variable, 33
- areaAndPerimeter function, 366
- arguments, 129, 132. See also parameters
- arithmetic expressions, 30, 45. See also expressions; arithmetic operators
- arithmetic operators
  - See also arithmetic expressions
  - assignment statements and, 94–99
  - described, 43
  - operator overloading and, 882–886
  - order of precedence and, 46–49
  - overview, 43–51
  - pointers and, 798–800
- array(s). See also specific types
  - base addresses, 521, 522–524
  - class objects, 655–657
  - components, accessing, 509–511, 545
  - in computer memory, 521–524
  - constant, 519–521
  - copy function and, 1413–1414
  - declaring, 510–511, 516–517, 527
  - graphs and, 1378–1380, 1388
  - implementation of queues as, 1176–1185
  - implementation of stacks as, 1128–1146
  - initializing, 512, 516–517, 548–550
  - largest element in, 512, 1005–1008
  - multidimensional, 543–544, 557–558
  - overview, 507–524
  - parallel, 542, 543
  - as parameters to functions, 518–521
  - passed by reference, 518
