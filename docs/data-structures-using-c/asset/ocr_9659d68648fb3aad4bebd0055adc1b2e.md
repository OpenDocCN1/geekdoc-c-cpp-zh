| | Initially empty | Insert 12 | Insert 01 | Insert 18 | Insert 56 | Insert 79 | Insert 49 |
|---|---|---|---|---|---|---|---|
| 0 | | | | | | | |
| 1 | | | 01 | 01 | 01 | 01 | 01 |
| 2 | | 12 | 12 | 12 | 12 | 12 | 12 |
| 3 | | | | | | | |
| 4 | | | | | | | |
| 5 | | | | | | | 49 |
| 6 | | | | | 56 | 56 | 56 |
| 7 | | | | | | | |
| 8 | | | | 18 | 18 | 18 | 18 |
| 9 | | | | | | 79 | 79 |

While inserting 49, the hashed location 9 is found occupied by key 79, so let us use Hash2(Key) = R – (Key MOD R), where R is a small prime number, even smaller than the table size. Let us use R = 7.

To insert 49, using Hash1(Key) = 49 % 10, we get 9 which is already occupied, so we use Hash2 as follows:

```
Hash2(49) = 7 – (49 % 7) = 7 – 0 = 7
```

Hence by double hashing,

```
Hash(49) = [Hash1(49) + Hash2(49)] % 10
= (9 + 7) % 10
= 6 and location 6 is not empty, so let us recompute again.
```

```
Hash(49) = [Hash1(49) + 2 x Hash2(49)] % 10
= 9 + 2 x 7
= 25 % 10
= 5 and is empty, so store key 49 there.
```

Example 11.5 illustrates the various types of open addressing.

**EXAMPLE 11.5** Given the input (4371, 1323, 6173, 4199, 4344, 9699, 1889) and hash function as Key % 10, show the results following:

+   1. Open addressing using linear probing
+   2. Open addressing using quadratic probing
+   3. Open addressing using double hashing h2(x) = 7 – (x MOD 7)

**Solution** The results are as follows: