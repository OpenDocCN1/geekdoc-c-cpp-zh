![](bbox=[0.27, 0.102, 0.735, 0.377])

**Figure 9.10** A hash table

# **NOTE:**

As of Java 8, the buckets change from linked lists into balanced binary trees when they get full. This improves performance if a hash function was poorly chosen and yields many collisions, or if malicious code tries to flood a hash table with many values that have identical hash codes.

# **TIP:**

If at all possible, the keys of a hash table should belong to a class that implements the `Comparable` interface. Then you are guaranteed not to suffer poor performance due to poorly distributed hash codes.

If you want more control over the performance of the hash table, you can specify the initial bucket count. The bucket count gives the number of