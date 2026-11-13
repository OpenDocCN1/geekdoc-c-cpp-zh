Since (d) and (f) may contain a few or many items, they may lead to variable-length records. Also, (e) may contain many items, unless it asks only for the highest level obtained.

# 1.4 Data base systems will be only briefly covered in this text. Why?

"Data base systems" refers to data stored in the secondary memory of the computer. The implementation and analysis of data structures in the secondary memory are very different from those in the main memory of the computer. This text is primarily concerned with data structures in main memory, not secondary memory.

# Data Structures and Operations

# 1.5 Give a brief description of (a) traversing, (b) sorting and (c) searching.

+   (a) Accessing and processing each record exactly once
+   (b) Arranging the data in some given order
+   (c) Finding the location of the record with a given key or keys

# 1.6 Give a brief description of (a) inserting and (b) deleting.

+   (a) Adding a new record to the data structure, usually keeping a particular ordering
+   (b) Removing a particular record from the data structure

# 1.7 Consider the linear array NAME in Fig. 1.15, which is sorted alphabetically.

+   (a) Find NAME[2], NAME[4] and NAME[7].
+   (b) Suppose Davis is to be inserted into the array. How many names must be moved to new locations.
+   (c) Suppose Gupta is to be deleted from the array. How many names must be moved to new locations?

![](bbox=[0.812, 0.516, 0.932, 0.732])

+   (a) Here NAME[K] is the kth name in the list. Hence,
+   NAME[2] = Clark, NAME[4] = Gupta, NAME[7] = Pace
+   (b) Since Davis will be assigned to NAME[3], the names Evans through Smith must be moved. Hence six names are moved.
+   (c) The names Jones through Smith must be moved up the array. Hence four names must be moved.

# 1.8 Consider the linear array NAME in Fig. 1.16. The values of FIRST and LINK[K] in the figure determine a linear ordering of the names as follows. FIRST gives the location of the first name in the list, and LINK[K] gives the location of the name following NAME[K], with 0 denoting the end of the list. Find the linear ordering of the names.