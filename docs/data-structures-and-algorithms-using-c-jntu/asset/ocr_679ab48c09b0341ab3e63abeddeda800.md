number could be conveniently manipulated, for example, truncated, to get the index of the key that is to be stored. Folding gives better spread of keys across the hash table. This process is fast and simple specially when bit patterns are used in place of numerical values. In the bit-oriented versions exclusive- or operations are applied.

Example: Consider a number 123456. Partition the number into three parts, 12 | 34 | 56. Add the three parts 12 + 34 + 56 = 112. Truncating the result gives 12, which is the index for the hash table to store the number 123456.

4. Extraction: In this method computing the address uses only a part of the key. From a student id 928324312 the method may use first four digits, 9283, or the last four digits, 4312, or the combination of the first two and last two digits, 9212, or any other combination. Every time only some part of the key is used. It is sufficient for hashing if this part is carefully chosen, only when the omitted part distinguishes the keys in an insignificant manner. For example, the starting digits of the ISBN code are the same for all the books of the same publisher. So, they must be excluded when computing the address if the data table has only the books from a single publisher.

# 8.5 COLLISIONS

When a hash function maps two different keys to same location then collision occurs. Thus the corresponding records cannot be stored in the same location. An array with four records, each with two fields, one for the key and one to hold data is considered. Let the hashing function be a simple modulus operation, i.e. array index is computed by finding the reminder of dividing the key by 4:

```
Array Index: = key MOD 4
```

Then key values 9, 13, 17 will all hash to the same index. When two (or more) keys hash to the same value, a collision is said to occur (Figure 8.8).

![](bbox=[0.15, 0.55, 0.85, 0.68])

Figure 8.8 Collision

Collision resolution techniques: The two most popular techniques for collision resolution are:

+   1. Separate chaining—An array of linked list implementation
+   2. Open addressing (or closed hashing)—Uses an array based implementation

# 8.5.1 SEPARATE CHAINING

The hash table is implemented as an array of linked lists. To insert an item into the table, it is appended to the corresponding linked lists. The linked list to which it is to be appended is determined by hashing the inserting item. This technique is known as chaining or separate chaining or open hashing because each hash table element is a separate chain (linked list). Its data field contains either keys or references to keys. This technique allows one to perform all operations easily without any collision. Separate chaining is depicted in Figure 8.9: