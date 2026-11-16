+   - The function should distribute the key apparently and randomly.
+   - It should distribute values uniformly over the address range and avoid collisions as far as possible. To uniformly distribute the values over the address range we have to know the address bound before define the hash function.

# ## 5.9 Overflow Resolution Technique --- Open Addressing

When a data item cannot be placed at the index calculated by the hash function (because of collision), we look for availability of another empty location in the hash table. This process is referred to as *open addressing*. Open addressing is generally used where storage space is large and hence it uses only the space in the hash table and does not use any space outside the hash table for storing the key values. In open addressing, arrays are used as storage for hash tables. Methods of open addressing includes,

+   - Linear probing (Open addressing).
+   - Quadratic probing.

# ## 5.9.1 Linear Probing

Linear probing method arises when there is no space for new value insertion. In order to solve this, the size of the table is increased and this change in the table size leads to change in the hash function.

For example, Let us use division function method, to find the hash address for the keys specified. Let the keys to be mapped in the hash table be 18, 72, 65, 34 and 13. Using the prime number 7, for the modulo operation, the hash address mapped for the keys are as follows,

```
H(18) = 18 % 7 = 4
H(72) = 72 % 7 = 2
H(65) = 65 % 7 = 2
H(34) = 34 % 7 = 6
H(13) = 13 % 7 = 6
```

| Index | Value |
| :--- | :--- |
| 0 | 13 |
| 1 | |
| 2 | 72 |
| 3 | 65 |
| 4 | 18 |
| 5 | |
| 6 | 34 |

Fig. 5.5 : Collision resolution using linear probing.

The first key (i.e., 18) will be mapped in the 4 position of the hash table. The next key (i.e., 72) will be mapped in the 2nd position of the hash table. The third key (i.e., 65) will try to map the key in the 2nd position of the hash table, since it is already mapped, it will search for the next free place, which is the 3rd position in the hash table. The fourth key (i.e., 34) will be mapped in the 6th position of the hash table. The fifth key (i.e., 13) will try to map the key in the 6th position of the hash table, since it is already mapped, it will search for the next free place, which is the 0th position (since the size of the hash table is 7) in the hash table.