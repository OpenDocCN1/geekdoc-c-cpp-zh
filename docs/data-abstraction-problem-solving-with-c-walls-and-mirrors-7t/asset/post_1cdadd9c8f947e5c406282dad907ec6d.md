
the prefix PlainBox:: to the method name. Observe that the prefix comes after the method's return type. The prefix is an extension of the method name only.

To create a PlainBox object in Python, you could use the following statement:

```
myBox = PlainBox("Jewelry");
```

C++ provides several forms for creating objects:

```
PlainBox myBox = PlainBox("Jewelry");
PlainBox myBox("Jewelry");
```

These statements are equivalent in C++ and create a PlainBox object that is local to the function or method in which it is created. In these examples, the C++ keyword new is not used.

The following example uses the keyword new to create a PlainBox object that exists until the programmer specifically deletes it:

```
PlainBox* someBoxPtr = new PlainBox("Jewelry");
```

Notice that PlainBox is followed by the * character to indicate that someBoxPtr is a pointer to a PlainBox object and is not the object itself. Pointers are discussed in more detail in C++ Interlude 2.

If an object in C++ is instantiated using the new operator, as in the example above, it is the responsibility of the programmer to delete that object from memory when it is no longer needed. In Python, garbage collection deletes unused objects and frees the memory that was used by those objects. C++ does not provide garbage collection, so you must free unused memory. To delete the object pointed to by someBoxPtr, use the statements

```
delete someBoxPtr; // Frees memory used by the object.
someBoxPtr = nullptr; // A safety precaution.
```

Each time you use the new operator to create an object, you must write a corresponding delete statement to free the object's memory. Otherwise, your application will have a memory leak.

Additional information about C++ classes appears in Section A.8 of Appendix A, Chapter 1, and in C++ Interludes 1 and 4.

*This page intentionally left blank*

## Index

- *, pointer variables, 121
- .h, header files, 32, 99–100
- ==, equality operator, 416–417, 495
- !=, inequality operator, 495
- ( ), algebraic expressions, 165–166, 171–172, 207–208
- ( ), predicate expressions, Python, 790
- *, return item operator, 495
- – –, move to previous item (prefix) operator, 495, 496
- , cpp implementation files, 32
- ;, functions declaration, 698
- @throws Javadoc tag, 232
- { }, compound statements, 700, 790
- { }, checking balance, 201–203
- – –, destructors, 146
- +, concatenation operator, overloading, 419–420
- ++, move to next item (postfix) operator, 495, 496
- < >, data types, 39
- <>, output stream operator, 421–423
- =, assignment operator, overloading, 417–419
- #define, 34–35
- #endif, 34–35
- #ifndef, 34–35

### A

- Abstract classes, 44–46, 343–346
- Abstract data types (ADT), 11–26, 96–98, 194–201, 241–255, 254–259, 348–352, 357–367, 373–395, 435–449, 503–506, 526–531, 606–611
  - array-based implementation, 96–98, 242–244
  - axioms, 200–201, 257–259
  - binary search trees, 442–449
  - binary trees, 435–442
  - core methods, 97–98
  - data structures and, 12–14
  - designing, 14–16
  - dictionaries, 526–531
  - graphs, 606–611
  - heaps, 503–506
  - implementation, 12, 16–17, 241–252
  - input line storage, 194
  - last in, first out (LIFO) property, 196–197
  - link-based implementation, 245–249
  - list specifications, 254–259, 348–352
  - operations, 15–16, 255–257, 348–350, 351–352, 438–441, 443–445, 527–529, 607
  - position-oriented, 389
  - priority queues, 379–381
  - queues, 373–395
  - solution design, 194–196
  - stacks, 194–201, 241–252
  - traversal operations, 436–438, 447–448, 529
  - Unified modeling language (UML), 14–15, 20
  - value-oriented, 389
- Access time, 154
- Accessor methods, 54
- Activation record, 54
- Addition operator, 102, 131–132, 139–140, 380, 440, 444, 464–465, 505, 528
- Adding a new entry/item, 471–473, 511–512
  - binary search trees, 471–473
  - heaps, 511–512
- Adjacency list and matrix, 608–611
- ADT bag, 17–26, 98–111, 131–132, 137–148
  - array-based implementation, 98–111
  - class-responsibility-collaborator (CRC), 18
  - constructors, 100–101, 139
  - core methods, 100–105, 139–142
  - header (h) files, 99–100, 138–139
  - identifying behavior, 18–19
  - interface template, 22–24
  - link-based implementation, 137–148
  - methods, 100–110, 139–148
  - operations, 21
  - resizable arrays, 131–132
  - specifications, 19–22
  - testing methods for, 110–111, 142
- advance function, 500
- Aggregation, 343
- Algebraic expressions, 164–172, 205–209, 428–429
  - binary trees and, 428–429
  - converting infix to postfix, 206–209
  - infix, 164–166, 205
  - parenthesis () for, 165–166, 171–172, 207–208
  - postfix, 165–166, 170–171, 205–206
  - prefix, 165–170
  - stacks with, 205–209
- Algorithm analysis, 3, 289–304, 305–332, 385–388, 471–481, 508–512, 577–579, 583–585, 622–625, 640–646, 682–684, 759–761
  - adding (inserting) a new entry/item, 471–473, 511–512, 583–585
  - analysis of, 291–300, 308–309, 311, 313–314, 317–319, 324–325
  - array-based implementation, 508–512
- Algorithms (cont'd)
  - average-case analysis, 298
  - balances trees, 577–579, 583–585
  - big O notation for, 294–298
  - binary search, 300–301
  - binary search trees, 471–481
  - cubic, 296
  - Dijkstra's shortest path, 624–625
  - efficiency of, 298–304, 305–332
  - event-driven simulations, 385–388
  - execution time, 292–293
  - exponential, 296
  - graph applications, 622–625
  - graph-traversal, 611
  - growth rate function (f(n)), 294, 297
  - growth rates, 293–294
  - heaps, 508–512, 683–684
  - insertion, 471–473, 577–579
  - linear, 296
  - merge sort, 314–319, 640–646
  - nested loops in, 292–294
  - order of, 294
  - parent-child relationships for, 471–480
  - perspective and, 298–300
  - Prim's minimum spanning tree, 622–623
  - priority queues and, 385–388
  - quadratic, 296
  - recurrence relations, 474–481, 508–511, 583–585
  - retrieving an entry/item, 481, 508
  - searching and compare, 682–683
  - searching, 300–301
  - sequence modification, 683
  - solution cost and, 290
  - sorting, 305–322, 683–684
  - standard template library (STL), 682–684
  - traversal of linked nodes, 292
  - verification of, 759–761
  - worst-case analysis, 298
- Alphabetical order of list names, 260–261
- Ancestor, tree relationships, 427
- Arithmetic expressions, 691
- Array-based implementation, 95–116, 153–154, 242–244, 266–272, 405–410, 456–458, 506–516, 534–536
  - abstract data type (ADT) approach, 96–98, 242–244
  - adding a new entry/item, 511–512
  - assertions, 98
  - bags, 98–111
  - binary trees, 456–458
  - circular array strategies, 405–407
  - core methods, 97–98, 100–105
  - dictionaries, 534–536
  - fixed-sized, 98
  - header (h) files, 99–100, 242–243, 266–267, 407–408, 512–513, 535
  - heaps, 506–516
  - link-based implementation compared to, 153–154, 410
  - lists, 266–272
  - methods, 100–114, 243–244, 268–272, 408–409, 513–516
  - nodes for, 456–458
  - queues, 405–410
  - recursion in, 112–114
  - removing entries/items, 107–110, 508–511
  - retrieving entries/items, 508
  - rightward drift strategy, 405
  - stacks, 242–244
  - testing methods for, 103–105, 110–111, 270
- ArrayBag class, 99–105
- ArrayDictionary class, 535–536
- ArrayQueue class, 408–409
- Arrays, 67–75, 130–132, 320, 486–487, 515–516, 673, 704–707, 783
  - allocation of, 130–132
  - binary search, 68–72, 486–487
  - box with reference argument, 71–72
  - const declaration for, 71
  - C++, 130–132, 704–707
  - dynamic allocation of, 130–132
  - heaps, transformation into, 515–516
  - Java programming, 783
  - largest value found in, 72–73
  - multidimensional, 706–707
  - one-dimensional, 704–705
  - partitioning, 74–75, 320
  - passing to functions, 705
  - recursion and, 67–75
  - resizable, 131–132
  - smallest value found in, 72–75
  - static allocation of, 130
  - STL operations, 675
  - target value, 68
  - tree sort of, 486–487
  - writing in backward order, 67
- as-a relationships, 340, 341–342
- ASCII character codes, 779
- Assertions, 98, 229–230, 759
- Assignment, 380–381, 417–419, 691–693
  - C++, 691–693
  - operator=, overloading, 417–419
  - tracking using priority queues, 380–381
- Associative containers, 678–681
- AVL trees, 597–599
- Axioms, 200–201, 257–259

### B

- Backtracking, 172–183, 211–212, 216
  - airline route search, 172–177, 211–212
  - directed path (graph), 173
  - eight queens problem, 177–183
  - exhaustive search, 173–177, 211–212
  - flight map operations, 175–176
  - implementation and, 180–183
  - recursion and, 172–183
  - stacks, 211–212, 216
- Backward order, 57–66
- Bag, ADT container, 17–24
- BagInterface class, 23–24, 151
- Balanced binary tree, 432, 597
- Balanced search trees, 567–602, 654–662
  - 2–3 trees, 569–585
  - 2–3–4 trees, 585–592
  - AVL trees, 597–599
  - B-trees, 654–662
  - dictionaries and, 654–662
  - external organization using, 654–662
  - inserting data into, 575–579, 587–591, 594–596, 597–599, 659–660
  - red-black trees, 592–596
  - removing data from, 579–585, 591, 594–596, 597–599, 660–662
  - rotation of, 597–599
  - searching, 572–574, 587, 594
  - splitting nodes, 589–591, 594–596
  - traversing, 572, 587, 594
  - tree height and balance of, 567–568, 597–599
- balancedAdd method, 464–465
- Base (degenerate) case, 49
- Base class (superclass), 40–44
- Big O notation, algorithm efficiency and, 294–298
- Binary file, 763, 772
- Binary search, 48–49, 68–72, 300–301, 486–487
  - arrays, 68–72, 486–487
  - algorithms, 300–301
  - recursive solutions using, 48–49
- Binary search trees, 429, 442–449, 471–487, 518, 533–534, 536–538
  - abstract data type (ADT), 442–449
  - adding a new entry, 471–473
  - algorithms for, 471–481
