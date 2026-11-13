After storing 22, 17, 32, 5, and 7, the table looks as shown in the left column of Table 11.9.

Table 11.9 Keys and quadratic probing

| Index | Key | | Index | Key |
|---|---|---|---|---|
| 0 | | | 0 | 24 |
| 1 | 22 | | 1 | 22 |
| 2 | 16 | insert 24 → | 2 | 16 |
| 3 | 17 | | 3 | 17 |
| 4 | 32 | | 4 | 32 |
| 5 | 5 | | 5 | 5 |
| 6 | | | 6 | |

We can see that while inserting 24, the address we get is

```
Hash(24) = 24 MOD 7
         = 3
```

It is also noted that the location 3 is already occupied.

We may now go for the quadratic function as

```
[Hash(24) - (1^2) MOD 7]
= (24 MOD 7) + 1 MOD 7
= (3 + 1) MOD 7 = 4 which is not occupied.
```

```
Hence, Hash(24) + (2^2) MOD 7
= (3 + 4) MOD 7 = 0
```

which is empty, so store 24 there.

# Double Hashing

Double hashing uses two hash functions, one for accessing the home address of a Key and the other for resolving the conflict. The sequence for probing is generated as follows:

```
(Hash1(Key), (Hash1(Key) + i x Hash2(Key)), .... i = 1, 2, 3, 4, ...
```

and the resultant address is modulo Max. Example 11.4 illustrates the double hashing concept.

EXAMPLE 11.4 Let the hash function be Key % 10, Max = 10, and the keys be 12, 01, 18, 56, 79, 49. Perform double hashing.

Solution Table 11.10 demonstrates all insertions and collision handling using double hashing.