
A hash table is useful for any graph theory problem where the nodes have real names instead of numbers. Here, as the input is read, vertices are assigned integers from 1 onward by order of appearance. Again, the input is likely to have large groups of alphabetized entries. For example, the vertices could be computers. Then if one particular installation lists its computers as bm1, bm2, bm3, ..., there could be a dramatic effect on efficiency if a search tree is used.

A third common use of hash tables is in programs that play games. As the program searches through different lines of play, it keeps track of positions it has seen by computing a hash function based on the position (and storing its move for that position). If the same position recurs, usually by a simple transposition of moves, the program can avoid expensive recomputation. This general feature of all game-playing programs is known as the transposition table.

Yet another use of hashing is in online spelling checkers. If misspelling detection (as opposed to correction) is important, an entire dictionary can be prehashed and words can be checked in constant time. Hash tables are well suited for this, because it is not important to alphabetize words; printing out misspellings in the order they occurred in the document is certainly acceptable.

Hash tables are often used to implement caches, both in software (for instance, the cache in your Internet browser) and in hardware (for instance, the memory caches in modern computers). They are also used in hardware implementations of routers.

We close this chapter by returning to the word puzzle problem of Chapter 1. If the second algorithm described in Chapter 1 is used, and we assume that the maximum word size is some small constant, then the time to read in the dictionary containing W words and put it in a hash table is O(W). This time is likely to be dominated by the disk I/O and not the hashing routines. The rest of the algorithm would test for the presence of a word for each ordered quadruple (row, column, orientation, number of characters). As each lookup would be O(1), and there are only a constant number of orientations (8) and characters per word, the running time of this phase would be O(R · C). The total running time would be O(R · C + W), which is a distinct improvement over the original O(R · C · W). We could make further optimizations, which would decrease the running time in practice; these are described in the exercises.

## Exercises

- 5.1 Given input {4371, 1323, 6173, 4199, 4344, 9679, 1989} and a hash function h(x) = x (mod 10), show the resulting
  - a. separate chaining hash table
  - b. hash table using linear probing
  - c. hash table using quadratic probing
  - d. hash table with second hash function h2(x) = 7 - (x mod 7)

- 5.2 Show the result of rehashing the hash tables in Exercise 5.1.

- 5.3 Write a program to compute the number of collisions required in a long random sequence of insertions using linear probing, quadratic probing, and double hashing.

- 5.4 A large number of deletions in a separate chaining hash table can cause the table to be fairly empty, which wastes space. In this case, we can rehash to a table half as large. Assume that we rehash to a larger table when there are twice as many elements as the table size. How empty should the table be before we rehash to a smaller table?

- 5.5 Reimplement separate chaining hash tables using a vector of singly linked lists instead of vectors.

- 5.6 The isEmpty routine for quadratic probing has not been written. Can you implement it by returning the expression currentSize==0?

- 5.7 In the quadratic probing hash table, suppose that instead of inserting a new item into the location suggested by findPos, we insert it into the first inactive cell on the search path (thus, it is possible to reclaim a cell that is marked deleted, potentially saving space).
  - a. Rewrite the insertion algorithm to use this observation. Do this by having findPos maintain, with an additional variable, the location of the first inactive cell it encounters.
  - b. Explain the circumstances under which the revised algorithm is faster than the original algorithm. Can it be slower?

- 5.8 Suppose instead of quadratic probing, we use “cubic probing”; here the ith probe is at hash(x) + i^3. Does cubic probing improve on quadratic probing?

- 5.9 Using a standard dictionary, and a table size that approximates a load factor of 1, compare the number of collisions produced by the hash function in Figure 5.4 and the hash function in Figure 5.5.

- 5.10 What are the advantages and disadvantages of the various collision resolution strategies?

- 5.11 Suppose that to mitigate the effects of secondary clustering we use as the collision resolution function f(i) = i · r(hash(x)), where hash(x) is the 32-bit hash value (not yet scaled to a suitable array index), and r(y) = [48271y (mod (2^31 - 1))] mod TableSize. (Section 10.4.1 describes a method of performing this calculation without overflows, but it is unlikely that overflow matters in this case.) Explain why this strategy tends to avoid secondary clustering, and compare this strategy with both double hashing and quadratic probing.

```
1 /**
2  * A good hash routine for string objects.
3  */
4 unsigned int hash( const string & key, int tableSize )
5 {
6    unsigned int hashVal = 2166136261;
7
8   for( char ch : key )
9      hashVal = ( hashVal ^ ch ) * 16777619;
10
11   return hashVal % tableSize;
12 }
```

Figure 5.5 Alternative hash function for Exercise 5.9.

- 5.12 Rehashing requires recomputing the hash function for all items in the hash table. Since computing the hash function is expensive, suppose objects provide a hash member function of their own, and each object stores the result in an additional data member the first time the hash function is computed for it. Show how such a scheme would apply for the Employee class in Figure 5.8, and explain under what circumstances the remembered hash value remains valid in each Employee.

- 5.13 Write a program to implement the following strategy for multiplying two sparse polynomials P1, P2 of size M and N, respectively. Each polynomial is represented as a list of objects consisting of a coefficient and an exponent. We multiply each term in P1 by a term in P2 for a total of MN operations. One method is to sort these terms and combine like terms, but this requires sorting MN records, which could be expensive, especially in small-memory environments. Alternatively, we could merge terms as they are computed and then sort the result. a. Write a program to implement the alternative strategy. b. If the output polynomial has about O(M + N) terms, what is the running time of both methods?

- * 5.14 Describe a procedure that avoids initializing a hash table (at the expense of memory).

- 5.15 Suppose we want to find the first occurrence of a string P1 P2 ... Pk in a long input string A1 A2 ... AN. We can solve this problem by hashing the pattern string, obtaining a hash value HP, and comparing this value with the hash value formed from A1 A2 ... Ak, A2 A3 ... Ak+1, ... AN-k+1 ... AN-k+2 ... AN. If we have a match of hash values, we compare the strings character by character to verify the match. We return the position (in A) if the strings actually do match, and we continue in the unlikely event that the match is false. * a. Show that if the hash value of A1 i+1 ... Ai+k-1 is known, then the hash value of A1 i+2 ... Ai+k can be computed in constant time. b. Show that the running time is O(k + N) plus the time spent refuting false matches. * c. Show that the expected number of false matches is negligible. d. Write a program to implement this algorithm. * e. Describe an algorithm that runs in O(k + N) worst-case time. ** f. Describe an algorithm that runs in O(N/k) average time.

- 5.16 A nonstandard C++ extension adds syntax that allows a switch statement to work with the string type (instead of the primitive integer types). Explain how hash tables can be used by the compiler to implement this language addition.

- 5.17 An (old-style) basic program consists of a series of statements numbered in ascending order. Control is passed by use of a goto or gosub and a statement number. Write a program that reads in a legal BASIC program and renumbers the statements so
