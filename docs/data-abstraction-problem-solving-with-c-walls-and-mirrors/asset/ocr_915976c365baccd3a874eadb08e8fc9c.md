+   5. A C++ compiler uses a symbol table to keep track of the identifiers that a program uses. When the compiler encounters an identifier, it searches the symbol table to see whether identifier has already been encountered. If it is new, it is inserted into the table. Thus, the symbol table needs only insertion and retrieval operations. Which implementation of the ADT dictionary would be most efficient as a symbol table?

+   6. Considering adding operations to the ADT dictionary to form the union and intersection of two dictionaries. Each operation returns a new dictionary. The union should combine all the entries in both dictionaries into a third dictionary. The intersection should be the entries common to both of the two dictionaries.

Within each dictionary, search keys are not repeated. However, an entry in one dictionary could have the same search key as an entry in the second dictionary. Propose and discuss ways to specify these two operations for this case.

+   7. The implementations of the ADT dictionary in this chapter make the following assumption: At any time, a dictionary contains at most one entry with a given search key. The definition of the ADT for a specific application may not allow duplicates; it is probably wise to test for them rather than simply assume they will not occur.

Modify the implementations so that they test for—disallow—any duplicates. What dictionary operations are affected? What are the implications for the unsorted linear implementations?

+   8. Although disallowing duplicate search keys in the ADT dictionary is reasonable for some applications, is it just for no application that will duplicate?

+   a. What are the implementations of inserting identical items with the same search key? What are the implications for the removal and retrieval operations?

+   b. What are the implementations of inserting items that are not identical but have the same search key? Specifically, what would the implementations of add, remove, and getitem do?

+   9. Suppose that you want to support two remove operations for the ADT dictionary—for example, removeByName and removeByID. Describe an efficient implementation for these operations.

+   10. Repeat Exercise 9, but use a binary search tree to organize one of the search keys and a sorted linked chain to organize the second key.

+   11. Can you use pseudocode for the dictionary operations, add, remove, and getitem when the implementation uses hashing and linear probing to resolve collisions.

+   12. Write the pseudocode for the remove operation when the implementation uses hashing and chaining to resolve collisions.

+   13. The success of a hash-table implementation of the ADT dictionary is related to the choice of a good hash function. A good hash function is easy to compute and will evenly distribute the data. Comment the appropriateness of the following hash functions. What patterns would hash to the same location?

+   14. The hash table has size 2,048. The search keys are English words. The hash function is
$h(key) = (Sum of positions in alphabet of key's letters) mod 2048

+   b. The hash table has size 2,048. The keys are strings that begin with a letter. The hash function is
$h(key) = (position in alphabet of first key) mod 2048

Thus, “BUT” maps to 2. How appropriate is this hash function if the strings are random? What if the strings are English words?