The probe sequence can be calculated as follows:

```
`probe = (probe + 1) mod size, where size indicates the table size`
```

Following is the stepwise execution of linear probing which is done by selecting a key value randomly:

+   1. Insert the key value 14. After the execution of the hash function on this key, it must be placed at the 4th position of the array, as follows:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
|   |   |   |   | 14|   |   |   |   |   |

+   2. Again the keys 15, 17, and 18 are placed at the 5th, 7th, and 8th positions of the array, respectively, as follows:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
|   |   |   |   | 14| 15|   | 17| 18|   |

+   3. Now, if we want to place the key 35, then it hashes to the position 5, which is already occupied. Linear probing resolves this collision by finding the next available empty slot. It finds the 6th position, which is empty, and places the key into that position, as follows:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
|   |   |   |   | 14| 15| 35| 17| 18|   |

+   4. Again, if we want to place the key 75, then it hashes to the position 5, which is already occupied. Therefore, the linear probing function finds the 6th position first, which is already occupied. Then, it finds the 7th position, which is also occupied. After that, it finds the 8th position, which is again occupied. At last, it finds an empty slot at the 9th position and places the key. The array after this operation would be as follows:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
|   |   |   |   | 14| 15| 35| 17| 18| 75|

Next, when we try to insert the keys 55, 65, and 95, each of these keys hashes to the same position as its predecessor and results in collision. This phenomenon is known as clustering. Therefore, instead of resolving the collision, this method first introduces the collision and then resolves it. This leads linear probing to be a very inefficient process, as it causes the number of collisions to be higher than expected. To resolve this, another technique was introduced, which is known as double hashing.

# Double Hashing

In double hashing, we calculate the probe sequence in a different way that sharply reduces the clustering. In this technique, the probe sequence is incremented by an amount based on the key value. Therefore, we use a second hash function to calculate the probe sequence, as follows:

```
`probe = (probe + DoubleHash(k)) mod size, where size indicates the table size`
```

Let's consider DoubleHash(k) = 1+(key mod 6) (Added 1 to ensure that the function never returns 0)

To explain this method, we use the our previous example, where the hash function is H(k) = k.

Following is the stepwise execution of double hashing, which is done by selecting a key value randomly:

+   1. The key 14 would be inserted using the normal hash function at the 4th position, as follows:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
|   |   |   |   | 14|   |   |   |   |   |