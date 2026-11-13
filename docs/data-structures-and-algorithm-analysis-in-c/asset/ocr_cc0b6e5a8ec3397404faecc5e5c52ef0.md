![](bbox=[0.2, 0.08, 0.85, 0.23])

+   * b. What is the running time of your program (there is a linear solution)?

+   4.47 * a. Show that via AVL single rotations, any binary search tree T1 can be transformed into another search tree T2 (with the same items).
+   * b. Give an algorithm to perform this transformation using O(N log N) rotations on average.
+   ** c. Show that this transformation can be done with O(N) rotations, worst-case.

+   4.48 Suppose we want to add the operation findKth to our repertoire. The operation findKth(k) returns the kth smallest item in the tree. Assume all items are distinct. Explain how to modify the binary search tree to support this operation in O(log N) average time, without sacrificing the time bounds of any other operation.

+   4.49 Since a binary search tree with N nodes has N + 1 nullPtr pointers, half the space allocated in a binary search tree for pointer information is wasted. Suppose that if a node has a nullPtr left child, we make its left child link to its inorder predecessor, and if a node has a nullPtr right child, we make its right child link to its inorder successor. This is known as a threaded tree and the extra links are called threads.
+   a. How can we distinguish threads from real children pointers?
+   b. Write routines to perform insertion and deletion into a tree threaded in the manner described above.
+   c. What is the advantage of using threaded trees?

+   4.50 Write a program that reads a C++ source code file and outputs a list of all identifiers (that is, variable names, but not keywords, that are not found in comments or string constants) in alphabetical order. Each identifier should be output with a list of line numbers on which it occurs.

+   4.51 Generate an index for a book. The input file consists of a set of index entries. Each line consists of the string IX, followed by an index entry name enclosed in braces, followed by a page number that is enclosed in braces. Each 1 in an index entry name represents a sublevel. A { represents the start of a range, and a } represents the end of the range. Occasionally, this range will be the same page. In that case, output only a single page number. Otherwise, do not collapse or expand ranges on your own. As an example, Figure 4.79 shows sample input and Figure 4.80 shows the corresponding output.