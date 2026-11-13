In our example, the table size is 811, so that the data array consists of 811 head pointers for 811 linked lists. Each list is a linked list where the nodes contain RecordType values.

Our class definition has one other private member variable, total_records, which keeps track of the total number of records in all 811 linked lists. You can complete this implementation yourself.

# Self-Test Exercises for Section 12.3

+   20. Consider the chaining version of the table that we have described. What value will the constructor place in each component of data?
+   21. Write the insert member function for the chaining version of the table.
+   22. Use your insert function to place six items in a hash table with a table size of 811. Use the keys 811, 0, 1623, 2435, 3247, and 2.
+   23. In our new table class, the array is still a fixed size. So why do we need the copy constructor, destructor, and overloaded assignment operator?
+   24. Suppose that the keys can be compared with the usual “less than” operator. Can you think of some advantage to keeping each linked list of the table sorted from smallest key to largest key?

# 12.4 TIME ANALYSIS OF HASHING

The worst case for hashing occurs when every key gets hashed to the same array index. In this unfortunate case, we may end up searching through all the items to find the one we are after—a linear operation, just like serial search. However, with some reasonable assumptions, the average time for a search of a hash table is dramatically fast, requiring us to examine just a handful of elements. This section provides the information needed for an average-time analysis of our three hashing methods.

# The Load Factor of a Hash Table

The average-time performance of hashing is complex, particularly if deletions are allowed. However, Knuth’s The Art of Programming, Volume 3, provides formulas that can guide our choice of hash-table algorithms. Knuth’s most useful formulas provide the average number of table elements that must be examined during a successful search for a key. There are three different formulas for the three versions of hashing: open addressing with linear probing, open addressing with double hashing, and chained hashing. These three formulas depend on how many items are in the table. When the table has many items, there are many collisions, and the average time for a search is longer. With this in mind, we first define a fraction called the load factor, which is written α and defined by the formula at the top of the next page.