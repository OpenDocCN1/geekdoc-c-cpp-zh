# 514 Appendix B Solutions to Exercises

![](bbox=[0.183, 0.09, 0.816, 0.385])

**Figure B-6:** Sorted chaining gives shorter average probe sequence lengths than chaining.

+   4. Example program LinearProbing implements a hash table that uses open address-ing with linear probing.
5. Example program QuadraticProbing implements a hash table that uses open addressing with quadratic probing.
6. Example program PseudoRandomProbing implements a hash table that uses open addressing with pseudo-random probing.
7. Example program DoubleHashing implements a hash table that uses open addressing with double hashing.
8. The probe sequences used by those algorithms will skip values if their stride evenly divides the size N. For example, suppose the table size is 10, and a value maps to location 1 with a stride of 2. Then its probe sequence visits positions 1, 3, 5, 7, and 9 then repeats. You can avoid this by ensuring that the stride cannot divide N. One way to do this is to make N prime so that no stride can divide it.
9. Example program OrderedQuadraticHashing implements a hash table that uses open addressing with ordered quadratic hashing.
10. Example program OrderedDoubleHashing implements a hash table that uses open addressing with double hashing.

Figure B-7 shows the average probe sequence lengths for the different open addressing algorithms have similar performance. All the nonordered algorithms have similar performance. Linear probing is generally slowest, but the others are within about one probe of giving the same performance. Double hashing has a slight advantage.