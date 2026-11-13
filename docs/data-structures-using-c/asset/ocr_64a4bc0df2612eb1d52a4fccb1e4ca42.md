The main idea behind universal hashing is to select the hash function at random at run-time from a carefully designed set of functions. Because of randomization, the algorithm can behave differently on each execution; even for the same input. This approach guarantees good average case performance, no matter what keys are provided as input.

# 11.4 COLLISION RESOLUTION STRATEGIES

No hash function is perfect. If Hash(Key1) = Hash(Key2), then Key1 and Key2 are synonyms and if bucket size is 1, we say that collision has occurred. As a consequence, we have to store the record Key2 at some other location. A search is made for a bucket in which a record is stored containing Key2, using one of the several collision resolution strategies. The collision resolution strategies are as follows:

+   1. Open addressing
+      (a) Linear probing
+      (b) Quadratic probing
+      (c) Double hashing
+      (d) Key offset
+   2. Separate chaining (or linked list)
+   3. Bucket hashing (defers collision but does not prevent it)

The most important factors to be taken care of to avoid collision are the table size and choice of the hash function. As we know, no hash function is perfect and we have a limitation on the table size too. Let us learn a few techniques to resolve this collision.

# 11.4.1 Open Addressing

In open addressing, when collision occurs, it is resolved by finding an available empty location other than the home address. If Hash(Key) is not empty, the positions are probed in the following sequence until an empty location is found. When we reach the end of table, the search is wrapped around to start and the search continues till the current collision location.

```
N(Hash(Key) + C(1)), N(Hash(Key) + C(2)), ..., N(Hash(Key) + C(i)), ... (11.1)
```

Here N is the normalizing function, Hash(Key) is the hashing function, and C(i) is the collision resolution (or probing) function with the ith probe. The normalizing function is required when the resulting index is out of range. A commonly used normalization function is MOD.

Closed hash tables use open addressing. In open addressing, all records are stored in the hash table itself also said to be resolving in the prime area which contains all home addresses. In case of chaining, the collisions are resolved by storing them at a separate area known as the overflow area.

In open addressing, when collision occurs, the table is searched for empty locations to store synonyms. Each table entry either contains a record or is empty. While searching