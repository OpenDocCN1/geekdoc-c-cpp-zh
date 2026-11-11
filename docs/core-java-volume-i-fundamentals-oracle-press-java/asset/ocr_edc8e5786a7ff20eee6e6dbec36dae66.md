such a way that objects with different data yield different codes. [Table 9.2](#) lists a few examples of hash codes that result from the `hashCode` method of the `String` class.

If you define your own classes, you are responsible for implementing your own `hashCode` method—see [Chapter 5](#) for more information. Your implementation needs to be compatible with the `equals` method. If `a.equals(b)`, then a and b must have the same hash code.

# Table 9.2 Hash Codes Resulting from the `hashCode` Method

| String | Hash Code |
|---|---:|
| "Lee" | 76268 |
| "lee" | 107020 |
| "eel" | 100300 |

What’s important for now is that hash codes can be computed quickly and that the computation depends only on the state of the object that needs to be hashed, not on the other objects in the hash table.

In Java, hash tables are implemented as arrays of linked lists. Each list is called a *bucket* (see [Figure 9.10](#)). To find the place of an object in the table, compute its hash code and reduce it modulo the total number of buckets. The resulting number is the index of the bucket that holds the element. For example, if an object has hash code 76268 and there are 128 buckets, then the object is placed in bucket 108 (because the remainder 76268 % 128 is 108). Perhaps you are lucky and there is no other element in that bucket. Then, you simply insert the element into that bucket. Of course, sometimes you will hit a bucket that is already filled. This is called a *hash collision*. Then, compare the new object with all objects in that bucket to see if it is already present. If the hash codes are reasonably randomly distributed and the number of buckets is large enough, only a few comparisons should be necessary.