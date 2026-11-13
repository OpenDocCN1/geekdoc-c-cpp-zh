
- 18. L. J. Guibas and R. Sedgewick, “A Dichromatic Framework for Balanced Trees,” Proceedings of the Nineteenth Annual IEEE Symposium on Foundations of Computer Science (1978), 8–21.
- 19. T. H. Hibbard, “Some Combinatorial Properties of Certain Trees with Applications to Searching and Sorting,” Journal of the ACM, 9 (1962), 13–28.
- 20. A. T. Jonassen and D. E. Knuth, “A Trivial Algorithm Whose Analysis Isn’t,” Journal of Computer and System Sciences, 16 (1978), 301–322.
- 21. P. L. Karlton, S. H. Fuller, R. E. Scroggs, and E. B. Kaehler, “Performance of Height Balanced Trees,” Communications of the ACM, 19 (1976), 23–28.
- 22. D. E. Knuth, The Art of Computer Programming: Vol. 1: Fundamental Algorithms, 3d ed., Addison-Wesley, Reading, Mass., 1997.
- 23. D. E. Knuth, The Art of Computer Programming: Vol. 3: Sorting and Searching, 2d ed., Addison-Wesley, Reading, Mass., 1998.
- 24. K. Melhorn, “A Partial Analysis of Height-Balanced Trees under Random Insertions and Deletions,” SIAM Journal of Computing, 11 (1982), 748–760.
- 25. K. Melhorn, Data Structures and Algorithms 1: Sorting and Searching, Springer-Verlag, Berlin, 1984.
- 26. J. Nievergelt and E. M. Reingold, “Binary Search Trees of Bounded Balance,” SIAM Journal on Computing, 2 (1973), 33–43.
- 27. A. J. Perlis and C. Thornton, “Symbol Manipulation in Threaded Lists,” Communications of the ACM, 3 (1960), 195–204.
- 28. S. Sen and R. E. Tarjan, “Deletion Without Rebalancing in Balanced Binary Trees,” Proceedings of the Twentieth Symposium on Discrete Algorithms (2010), 1490–1499.
- 29. D. D. Sleator and R. E. Tarjan, “Self-adjusting Binary Search Trees,” Journal of the ACM, 32 (1985), 652–686.
- 30. D. D. Sleator, R. E. Tarjan, and W. P. Thurston, “Rotation Distance, Triangulations, and Hyperbolic Geometry,” Journal of the AMS (1988), 647–682.
- 31. R. E. Tarjan, “Sequential Access in Splay Trees Takes Linear Time,” Combinatorica, 5 (1985), 367–378.
- 32. A. C. Yao, “On Random 2–3 Trees,” Acta Informatica, 9 (1978), 159–170.

This page intentionally left blank

## Hashing

In Chapter 4 we discussed the search tree ADT, which allowed various operations on a set of elements. In this chapter, we discuss the **hash table** ADT, which supports only a subset of the operations allowed by binary search trees.

The implementation of hash tables is frequently called **hashing**. Hashing is a technique for performing insertions, deletions, and finds in constant average time. Tree operations that require ordering information among the elements are not supported efficiently. Thus, operations such as `findMin`, `findMax`, and the printing of the entire table in sorted order in linear time are not supported.

The central data structure in this chapter is the **hash table**. We will ...

- See several methods of implementing the hash table.
- Compare these methods analytically.
- Show numerous applications of hashing.
- Compare hash tables with binary search trees.

### 5.1 General Idea

The ideal hash table data structure is merely an array of some fixed size containing the items. As discussed in Chapter 4, generally a search is performed on some part (that is, data member) of the item. This is called the **key**. For instance, an item could consist of a string (that serves as the key) and additional data members (for instance, a name that is part of a large employee structure). We will refer to the table size as `TableSize`, with the understanding that this is part of a hash data structure and not merely some variable floating around globally. The common convention is to have the table run from 0 to `TableSize` - 1; we will see why shortly.

Each key is mapped into some number in the range 0 to `TableSize` - 1 and placed in the appropriate cell. The mapping is called a **hash function**, which ideally should be simple to compute and should ensure that any two distinct keys get different cells. Since there are a finite number of cells and a virtually inexhaustible supply of keys, this is clearly impossible, and thus we seek a hash function that distributes the keys evenly among the cells. Figure 5.1 is typical of a perfect situation. In this example, `john` hashes to 3, `phil` hashes to 4, `dave` hashes to 6, and `mary` hashes to 7.

![](img/e449061a0cac9cafaefd979fab665b33_212_0.png)

This is the basic idea of hashing. The only remaining problems deal with choosing a function, deciding what to do when two keys hash to the same value (this is known as a collision), and deciding on the table size.

### 5.2 Hash Function

If the input keys are integers, then simply returning Key mod TableSize is generally a reasonable strategy, unless Key happens to have some undesirable properties. In this case, the choice of hash function needs to be carefully considered. For instance, if the table size is 10 and the keys all end in zero, then the standard hash function is a bad choice. For reasons we shall see later, and to avoid situations like the one above, it is often a good idea to ensure that the table size is prime. When the input keys are random integers, then this function is not only very simple to compute but also distributes the keys evenly.

Usually, the keys are strings; in this case, the hash function needs to be chosen carefully. One option is to add up the ascii values of the characters in the string. The routine in Figure 5.2 implements this strategy.

The hash function depicted in Figure 5.2 is simple to implement and computes an answer quickly. However, if the table size is large, the function does not distribute the keys well. For instance, suppose that TableSize = 10,007 (10,007 is a prime number). Suppose all the keys are eight or fewer characters long. Since an ascii character has an integer value that is at most 127, the hash function typically can only assume values between 0 and 1,016, which is 127 * 8. This is clearly not an acceptable distribution!

Another hash function is shown in Figure 5.3. This hash function assumes that Key has at least three characters. The value 27 represents the number of letters in the English alphabet, plus the blank, and 729 is 27^2. This function examines only the first three characters, but if these are random and the table size is 10,007, as before, then we would expect a

```
int hash( const string & key, int tableSize )
{
   int hashVal = 0;
   for( char ch : key )
      hashVal += ch;
   return hashVal % tableSize;
}

Figure 5.2 A simple hash function
```

```
int hash( const string & key, int tableSize )
{
   return ( key[ 0 ] + 27 * key[ 1 ] + 729 * key[ 2 ] ) % tableSize;
}

Figure 5.3 Another possible hash function—not too good
```

reasonably equitable distribution. Unfortunately, English is not random. Although there are 26^3 = 17,576 possible combinations of three characters (ignoring blanks), a check of a reasonably large online dictionary reveals that the number of different combinations is actually only 2,851. Even if none of these combinations collide, only 28 percent of the table can actually be hashed. Thus this function, although easily computable, is also not appropriate if the hash table is reasonably large.

Figure 5.4 shows a third attempt at a hash function. This hash function involves all characters in the key and can generally be expected to distribute well (it computes \sum_{i=0}^{KeySize-1} Key[KeySize - i - 1] * 37^i and brings the result into proper range. The code computes a polynomial function (of 37) by use of Horner's rule. For instance, another way of computing h_0 = k_0 + 37k_1 + 37^2 k_2 is by the formula h_k = ((k_2) * 37 + k_1) * 37 + k_0. Horner's rule extends this to an nth degree polynomial.

```
/**
 * A hash routine for string objects.
 */
unsigned int hash( const string & key, int tableSize )
{
   unsigned int hashVal = 0;
   for( char ch : key )
      hashVal = 37 * hashVal + ch;
   return hashVal % tableSize;
}

Figure 5.4 A good hash function
```
