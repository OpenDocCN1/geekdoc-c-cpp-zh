# FIGURE 12.8 Average Number of Table Elements Examined During a Successful Search

| Load factor (α) | Open addressing with linear probing 1/2 (1 + 1/(1-α)) | Open addressing with double hashing -ln(1-α)/α | Chained hashing 1 + α/2 |
|---|---|---|---|
| 0.5 | 1.50 | 1.39 | 1.25 |
| 0.6 | 1.75 | 1.53 | 1.30 |
| 0.7 | 2.17 | 1.72 | 1.35 |
| 0.8 | 3.00 | 2.01 | 1.40 |
| 0.9 | 5.50 | 2.56 | 1.45 |
| 1.0 | | | 1.50 |
| 2.0 | \multicolumn{2}{c}{Not applicable} | 2.00 |
| 4.0 | | | 3.00 |

# Self-Test Exercises for Section 12.4

+   25. Suppose that you place 180 items in a hash table with an array size of 200. What is the load factor? For each of the three hash methods, what is the average number of table elements that you expect to have examined during a successful search?

+   26. You want to place 1000 elements in a hash table, and you'd like an average search to examine just two table elements. How big does the table's array need to be? Give separate answers for the three hash methods.

# 12.5 PROGRAMMING PROJECT: A TABLE CLASS WITH STL VECTORS

# A New Table Class

We have discussed table classes implemented with an array of records (for open-address hashing) and an array of linked lists (for chained hashing). A table class can also be implemented with existing STL containers. This is advantageous in that the table can easily access and modify data items using the member functions of the containers. We suggest the STL vector class to implement a new version of the table class. The STL vector class is analogous to a dynamic array for which certain member functions automatically increase the size of the array. It uses subscripting to access elements (such as v[2] = 10 for a vector v of integer values). Appendix H provides details for using the vector template class. Like the table in Figure 12.7 on page 616, this table will use chained hashing, but there are a few changes in the design.