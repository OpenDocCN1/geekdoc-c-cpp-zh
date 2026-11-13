In a course that has time for advanced tree projects (Chapter 11), we analyze the recursive tree algorithms, explaining the importance of keeping the trees balanced—both to improve worst-case performance, and to avoid potential run-time stack overflow.

**Searching and sorting.** Chapters 12 and 13 provide fundamental coverage of searching and sorting algorithms. The searching chapter reviews binary search of an ordered array, which many students will have seen before. Hash tables also are introduced in the search chapter. The sorting chapter reviews simple quadratic sorting methods, but the majority of the chapter focuses on faster algorithms: the recursive merge sort (with worst-case time of O(n log n)), Tony Hoare's recursive quicksort (with average-time O(n log n)), and the tree-based heap sort (with worst-case time of O(n log n)). There is also a new introduction to the C++ Standard Library sorting functions.

# Advanced Projects

The text offers good opportunities for optional projects that can be undertaken by a more advanced class or by students with a stronger background in a large class. Particular advanced projects include the following:

+   - A polynomial class using dynamic memory (Section 4.6).
+   - An introduction to Standard Library iterators, culminating in an implementation of an iterator for the student's bag class (Sections 6.3 through 6.5).
+   - An iterator for the binary search tree (Programming Projects in Chapter 10).
+   - A priority queue, implemented with a linked list (Chapter 8 projects), or implemented using a heap (Section 11.1).
+   - A set class, implemented with B-trees (Section 11.3). We have made a particular effort on this project to provide information that is sufficient for students to implement the class without need of another text. In our courses, we have successfully directed advanced students to do this project as independent work.
+   - An inheritance project, such as the ecosystem of Section 14.2.
+   - An inheritance project using an abstract base class such as the game base class in Section 14.3 (which allows easy implementation of two-player games such as Othello or Connect Four).
+   - A graph class and associated graph algorithms from Chapter 15. This is another case where advanced students may do work on their own.