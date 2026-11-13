# Double Hashing to Reduce Clustering

Consider what happens during an insertion with a collision. The insertion function moves forward from the original index until a vacant spot is found in the array. For example, suppose that a new key hashes to location 330, but this location is full. Then the insertion tries 331, then 332, then 333, and so on. Searching for a vacant spot in this manner is called **linear probing**.

There is a problem with linear probing: When several different keys are hashed to the same array location, the result is a small cluster of elements, one after another. As the table approaches its capacity, these clusters tend to merge into larger and larger clusters. This is the problem of **clustering**. If the key values happen to be consecutive numbers (such as a run of consecutive stock numbers in an inventory), then a “division hash function” makes clustering even worse. As clustering gets worse, insertions take longer because the insert function must step all the way through a cluster to find a vacant location. Elements are inserted farther and farther from their correct hashed index, and searches require more time.

The most common technique to avoid clustering is called **double hashing**. The technique uses a second hash function to determine how we move through an array to resolve a collision. To see how this works, let’s call the original hash function hash1, and call the second hash function hash2. When an item is inserted, double hashing begins by hashing the key to an array index using hash1. If there is a collision, then we calculate hash2(key) using the result to tell us how far to move through the array in looking for a vacant spot. For example, suppose that a new key hashes to location 330, and that hash2(key) is 7. If location 330 is occupied, then we move forward 7 spots and try location 337. If 337 is also occupied, then we move forward another 7 spots to location 344, and so on.

As we are stepping through the array, adding hash2(key) to the index at each step, there are two considerations:

+   * The array index must not leave the valid range of 0 to CAPACITY - 1. We can keep the index in this range with the “%” operation. In particular, suppose that i is the index that we have just examined (with a collision). Then the next index to examine is

```
(i + hash2(key)) % CAPACITY
```

For example, suppose that CAPACITY is 811, and hash2(key) is 14. If a new key hashes to spot 787, and there is a collision, then the next few spots that we will try are 801, then 4, then 18, then 32. Notice that the 4 is calculated as (801 + 14) % CAPACITY.

+   * As we step through the array, we must ensure that every array position is examined. With double hashing, this is a potential problem. We could come back to our starting position before we have examined every available location. There is an easy way to avoid this problem: Make sure that