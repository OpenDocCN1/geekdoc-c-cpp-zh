# Hash Table

| | Overflow |
|---|---|
| 0 | 1000 | 1057 |
| | 9530 | |
| 1 | | |
| 2 | 9877 | |
| | 2007 | |
| 3 | 3013 | |
| 4 | 9879 | |

**Figure 9.4** An illustration of bucket hashing for seven numbers in a five-bucket hash table using the hash function $h(K) = K \pmod 5$. Each bucket contains two slots. The numbers are inserted in the order 9877, 2007, 1000, 3013, 9879, and 1057. Two of the values hash to bucket 0, three values hash to bucket 2, and one value hashes to bucket 4. Bucket 2 cannot not hold two values, the third ends up in the overflow bucket.

buckets share the overflow bucket. A good implementation will use a hash function that distributes the records among the buckets so that as few records as possible go into the overflow bucket. Figure 9.4 illustrates bucket hashing.

When searching for a record, the first step is to hash the key to determine which bucket should contain the record. The records in that bucket are then searched. If the desired key is not found and the bucket has free slots, then the search is complete. If the bucket is full, then it is possible that the desired record is stored in the overflow bucket. In this case, the overflow bucket must be searched until the record is found or all records in the overflow bucket have been checked. If many records are in the overflow bucket, this will be an expensive process.

A simple variation on bucket hashing is to hash a key value to the hash table as though buckets were not being used. If the home position is full, then the collision resolution process is to move down the table towards the end of the bucket while searching for a free slot in which to store the record. If the bottom of the bucket is reached, then the collision resolution routine wraps around the top of the bucket to continue the search for an open slot. For example, assume that buckets contain eight records, with the first bucket being contains of slots 0 through 7. If a record is hashed to slot 5, the collision resolution process will attempt to insert the record into the table in the order 5, 6, 7, 0, 1, 2, 3, and finally 4. If all slots in this bucket are full, then the record is assigned to the overflow bucket.