is about twice as big and scan down the entire original hash table, compute the new hash value for each record, and insert them in a new table. For example, if initially, the table is of size 7 and the hash function is key % 7 then, this would be as shown in Table 11.14. As the table is more than 70% full, a new table is created (Table 11.15) and the values are inserted in the new table. The size of the new table is 17, that is next prime of double of 7 that is 14. Rehashing is very expensive, as its running time is O(N).

| | |
|---|---|
| Insert 7, 15, 3, 74, 73 | |
| 0 | 7 |
| 1 | 15 |
| 2 | |
| 3 | 73 |
| 4 | 74 |
| 5 | |
| 6 | 13 |

| | |
|---|---|
| 0 | |
| 1 | |
| 2 | |
| 3 | |
| 4 | |
| 5 | 73 |
| 6 | 74 |
| 7 | 7 |
| 8 | |
| 9 | |
| 10 | |
| 11 | |
| 12 | |
| 13 | 13 |
| 14 | |
| 15 | 15 |
| 16 | |

# 11.4.2 Chaining

We have discussed three techniques that are used to compute probe sequences (to relocate synonyms) namely, linear probing, quadratic probing, and rehashing. Of course, we can store the linked lists inside the hash table, in the unused hash table slots. The technique used to handle synonyms is chaining; it chains together all the records that hash to the same address. Instead of relocating synonyms, a linked list of synonyms is created whose head is the home address of synonyms. In Chapter 6, we have discussed implementing a linked list within an array. However, we need to handle pointers to form a chain of synonyms. The extra memory is needed for storing pointers.