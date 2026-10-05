434

Chap. 12 Lists and Arrays Revisited

![](bbox=[0.2465, 0.1865, 0.7535, 0.2965])

**Figure 12.19** Some example multilists.

[Stal11b]. You can get more information about Java’s garbage collection system **The Java Programming Language** by Ken Arnold and James Gosling [AG06].

For more details on sparse matrix representations, the Yale representation is described by Eisenstat, Schultz and Sherman [ES81]. The MATLAB sparse matrix representation is described by Gilbert, Mer, and Schreiber [GMS91].

An introductory text on operating systems covers many topics relating to memory issues, including layout of files on disk and caching of information in main memory. All of the topics covered here on memory management, buffer pools, and paging are relevant to operating system implementation. For example, we *Operating Systems* by William Stallings[Stal11a].

# 12.5 Exercises

+   12.1 For each of the following bracket notation descriptions, draw the equivalent multilist in graphical form as shown in Figure 12.2.

+   (a, b), (c, d, e), (f, g), h)
(a, b), (c, d, L1:e1)
(c) L1:a, L1:b2, L2, L1)

+   12.2 Show the bracket notation for the list of Figure 12.19(a).

+   Show the bracket notation for the list of Figure 12.19(b).

+   Show the bracket notation for the list of Figure 12.19(c).

+   12.3 Given the linked representation of a list such as

$$(x_1, y_1, y_2, \langle z_1, z_2 angle, y_4, \langle w_1, w_2 angle, x_4)$$

write an in-inverse bracket to resolve the subsets at all levels including the topmost level. For this example, the result would be a linked representation corresponding to

$$(x_4, \langle w_2, w_1 angle, y_4, \langle z_2, z_1 angle, y_2, y_1), x_1)$$

+   12.4 What fraction of the values in a matrix must be zero for the sparse matrix representation of Section 12.2 to be more space efficient than the standard two-dimensional matrix representation when data require eight bytes, array indices require two bytes, and pointers require four bytes?