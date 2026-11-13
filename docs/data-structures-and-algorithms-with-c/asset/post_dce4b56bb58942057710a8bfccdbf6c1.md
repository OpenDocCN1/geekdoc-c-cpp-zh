
```
Set HashIndex = HashIndex mod size
[End of Loop]
d) If HashTable[HashIndex] = NULL then
    Set HashTable[HashIndex] = Key
    Set flag[HashIndex] = 1
[End of if]
[End of IF]
3. Return
```

## Double Hashing

Double hashing is a popular collision resolution technique in open addressed hash table. It uses two hash functions:

- i) Like linear probing First hash function H is used as a starting address and
- ii) Second hash function H' is used to find out the interval to skip a variable amount. Suppose a record R with key K has the hash address H(K) = h and H'(K) = h' ≠ m, then we search the location with the address h, h + h', h + 2h', h + 3h'...
- If m is a prime number, then the above sequence will access all the location in the table T.

Second hash function in double hashing has the following couple of requirements

- It must never evaluate to 0.
- Must make sure that all cells can be probed.

A popular hash function for double hashing is Hash2(key) = R - (key % R) where R is a prime number that is smaller than the size of the table.

## Example:

Suppose input keys {89, 18, 49, 58, 69} and table size:10
Largest prime number less than 10 is 7
Hash1(key) = key % 10 and Hash2(key) = 7 - (key % 7)
Hash(89) = 89 % 10 = 9
Hash1(18) = 18 % 10 = 8
Hash1(49) = 49 % 10 = 9, collision occur
Hash2(49) = 7 - (49 % 7) = 7 position move from [9]
Hash1(58) = 58 % 10 = 8, collision occur
Hash2(58) = 7 - (58 % 7) = 5 position move from [8]
Hash1(69) = 69 % 10 = 9, collision occur
Hash2(69) = 7 - (69 % 7) = 1 position move from [9]

| Index | Value |
|---|---|
| [0] | 69 |
| [1] | |
| [2] | |
| [3] | 58 |
| [4] | |
| [5] | |
| [6] | 49 |
| [7] | |
| [8] | 18 |
| [9] | 89 |

Figure 11.4: Double Hashing

## Advantage:

- It effectively eliminates clustering.
- It can allow the table to become nearly full.

## Disadvantage

The main drawback of this method is in the implementation of deletion.

## Insertion a key in a Hash Table using Double Probing

Following algorithm describes the process of inserting a key in a hash table using a Double Probing collision resolution technique.

## Algorithm of Insertion in Double Probing

```
Algorithm: INSERT_DOUBLE_PROB(HashTable, Key, Size)
(HashTable is an array represents a hash table, Key is a searching key and Size is the size of the HashTable)
1. Set HashIndex = Key mod size
   Set Flag[HashIndex] = false
2. If HashTable[HashIndex] = NULL then
   a) Set HashTable[HashIndex] = Key
   b) Set Flag[HashIndex] = true
   else
   i) Set move = prime - (Key mod prime)
   ii) set count = 1
   iii)Repeat while HashTable[HashIndex] != NULL
   a) Set HashIndex = HashIndex + count * move
   b) Set HashIndex = HashIndex mod size
   c) set count=count+1
   [End of Loop]
   iv) Set HashTable[HashIndex] = Key
   v) Set Flag[HashIndex] = true
   [End of IF]
3. Return
```

## Separate Chaining

In this technique, each bucket is independent and has the same sort of list of entries with the same key value. The time for hash table operation is the time to find the bucket, in addition, the time for the list operation.

Suppose, the hash table contains m slots. Each slot in the hash table contains a pointer to a linked list (separate chain) and the list stores the elements hashed to that slot. Hence, this method is known as Separate Chaining. A new key can be placed anywhere within a chain, as no ordering among the keys is used. As such, the new node is inserted at the end of a chain.

The hash table containing m pointers can be defined as follows:

```
node *hash[m];
```

## Example:

Suppose input keys are {20, 10, 1, 44, 64, 36, 30, 17, 46}; and hash function h(K) = K mod 10.

![](img/723fa3ef35f5102eb67dc45b74bb823d_320_0.png)

```
hashkey = key % table size
0=20%10
0=10%10
1=1%10
4=44%10
4=44%10
4=64%10
6=36%10
0=30%10
7=17%10
6=46%10
```

## Figure 11.5: Separate Chaining

The main drawback to chaining is that one needs more memory spaces for the link field and there are m memory slots for the pointer array. An additional disadvantage is that traversing a linked list has poor cache representation.

- Cost is proportional to the length of the list: Cost in terms of time complexity is proportional to the length of the list.
- Worst case: If the hash function is not efficient then it generates same hash key that increases the length of one list.
- M too large: If the value of m is too large then the number of chains becomes a more and more chain will be empty.
- M too small: If the value of m is too small, that increase the length of the list.

## Table 11.2: Type of Collision Resolution Technique

| Feature | Linear Probing | Quadratic Probing | Double Hashing |
| :--- | :--- | :--- | :--- |
| Efficiency | Fastest among three. | Easy to implement and deploy | Make more efficient use of memory |
| Probe use | Use few probes. | Uses extra memory for links and it does not probe all locations in the table. | Use few probes, but take more time. |
| Demerit | Primary clustering is a limitation. | Secondary clustering is the limitation. | More complicated to implement. |
| Computing Interval | The interval between probes is fixed and it is 1. | The interval between probes increases proportionally to the hash value. | The interval between probes is computed using the second hash function. |

## Problems for which Hash Tables are not suitable are:

- The problem for which data ordering is required.
- Problems having multi-dimensional data.
- Prefix searching if keys are long and of variable length.
- The problem that has dynamic data.
- The problem in which data does not have any unique key.

## Advantages of Hash Table

- It can efficiently handle a large volume of data.
- The speed of searching a data item increased as parallel searching can be applied here.
- Look up cost may be reduced by proper hash function, hash table size and internal data structure.

## Disadvantages of Hash Table

- Hash table implementation is more difficult than search tree.
- Hash table does not allow duplicate keys.
- In some cases, the cost of a good hash function is more than that of the search tree.
- For a dynamic hash table cost of insertion and searching of the element in the hash table is more.
- If collision occurs very frequently in the hash table then the efficiency of hash table degrades.

## Load Factor

The performance of hash table depends on two factors, initial capacity and load factor. Initial capacity is the number of cells(n) in the hash table. A Load Factor (α) of a hash table is defined as the ratio of the number of elements (n) in the hash table to the table size (size).

α = n / size

Load Factor is a measure which decides when exactly to increase the hash table capacity, so that get and put operation can still have O(1) complexity.

For linear probing α can tends to 1 (0 ≤ α ≤ 1), that implies collision probability is higher in linear probing. Load Factor tends to zero (0) implies that the proportion of unused space on hash table is increasing. However, there is no necessary reduction in search cost. The result is wasted memory.

Generally, the default load factor (0.75) indicates better performance for a hash table. The expected number of entries in the hash table and its load factor should be considered when the initial capacity of the hash table is defined. If the initial capacity is more than the maximum number of entries divided by the load factor, no rehash operation will ever occur.

## Summary

- Hashing is one of the most suitable techniques for storing and retrieving data when data volume is more than the storage volume.
- The choice of best hash function depends on the application.
- Collision resolution is one of the key feature of hashing process.

## Exercises

1. What do you mean by hashing? What are the applications where you will prefer hash tables to other data structures?
2. Why do the hash functions need to be simple?
