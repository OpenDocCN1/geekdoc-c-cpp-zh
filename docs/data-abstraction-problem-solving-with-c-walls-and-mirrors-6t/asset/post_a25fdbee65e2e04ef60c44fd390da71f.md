
## Average-case efficiency of retrievals and removals

Some searches of the hash table are unsuccessful because the relevant chain is empty. Such searches are virtually instantaneous. For an unsuccessful search of a nonempty chain, however, getItem and remove must examine the entire chain, or α items in the average case. On the other hand, a successful search must examine a nonempty chain. In the average case, the search will locate the item in the middle of the chain. That is, after determining that the linked chain is not empty, the search will examine α / 2 items. Thus, the efficiency of the retrieval and removal operations under the separate-chaining approach is 1 + α/2 for a successful search, and 1 + α for an unsuccessful search.

Even if the linked chains typically are short, you should still estimate the worst case. If you seriously underestimate tableSize, or if most of the dictionary items happen to hash into the same location, the number of items in a chain could be quite large. In fact, in the worst case, all n items in the dictionary could be in the same linked chain!

As you can see, the time that a retrieval or removal operation requires can range from almost nothing—if the linked chain to be searched either is empty or has only a couple of items in it—to the time required to search a chain that contains all the items in the dictionary, if all the items hashed into the same location.

**Comparing techniques.** Figure 18-15 plots the relative efficiency of the collision-resolution schemes just discussed. When the hash table is about half full—that is, when α is 0.5—the techniques are nearly equal in efficiency. As the dictionary fills and α approaches 1, separate chaining is the most efficient technique. Does this mean that we should discard all other search algorithms in favor of hashing with separate chaining? No. The analyses here are average-case analyses. Although an implementation of the ADT dictionary that uses hashing might often be faster than one that uses a search tree, in the worst case it can be much slower. If you can afford both an occasional slow search and a large $TableSize$—that is, a small $\alpha$—then hashing can be an attractive dictionary implementation. However, if you are performing a life-and-death search for your city's poison control center, a search-tree implementation would at least provide you with a guaranteed limit on its worst-case behavior.

In the worst case, a hashing implementation of a dictionary can be much slower than other implementations

Furthermore, while separate chaining is the most time-efficient collision-resolution scheme, you do have the storage overhead of the pointers in the linked chain. If the data entries in the dictionary are small, the pointers add a significant overhead in storage, and you may want to consider a simpler collision-resolution scheme. On the other hand, if the entries are large, the addition of a pointer is insignificant, so separate chaining is a good choice.

### Note: Maintaining the performance of hashing

Collisions and their resolution typically cause the load factor $\alpha$ to increase and the efficiency of the dictionary operations to decrease. To maintain efficiency, you should restrict the size of $\alpha$ as follows:
- $\alpha < 0.5$ for open addressing
- $\alpha < 1.0$ for separate chaining

Should the load factor exceed these bounds, you must increase the size of the hash table using rehashing.

## 18.4.4 What Constitutes a Good Hash Function?

Before we conclude this introduction to hashing, consider in more detail the issue of choosing a hash function to perform the address calculations for a given application. A great deal has been written on this subject, most of which is beyond the mathematical level of this book. However, this section will present a brief summary of the major concerns.

- Is the hash function easy and fast to compute? If a hashing scheme is to perform dictionary operations almost instantaneously and in constant time, you certainly must be able to calculate the hash function rapidly. Most of the common hash functions require only a single division (like the modulo operation), a single multiplication, or some kind of “bit-level” operation on the internal representation of the search key. In all these cases, the requirement that the hash function be easy and fast to compute is satisfied.

- Does the hash function scatter the data evenly throughout the table? Unless you use a perfect hash function—which is usually impractical to construct—you typically cannot avoid collisions entirely. For example, to achieve the best performance from a separate-chaining scheme, each entry $table[i]$ should point to a chain containing approximately the same number of items; that is, each chain should contain approximately $n / tableSize$ items (and thus no chain should contain significantly more than $n / tableSize$ items). To accomplish this goal, your hash function should scatter the search keys evenly throughout the hash table.

You cannot avoid collisions entirely

- How well does the hash function scatter random data? If every search-key value is equally likely, will the hash function scatter the search keys evenly? For example, consider nine-digit employee ID numbers as the search keys, a hash table $table[0..39]$, and a hash function $h(x) = (\text{first two digits of } x) \mod 40$. If all employee ID numbers are equally likely, does a given ID number $x$ have equal probability of hashing into any one of the 40 array locations? For this hash function, the answer is no. Only ID numbers that start with 19, 59, and 99 map into table[19], while only ID numbers that start with 20 and 60 map into table[20]. In general, three different ID prefixes—that is, the first two digits of an ID number—map into each array location 0 through 19, while only two different prefixes map into each array location 20 through 39. Because all ID numbers are equally likely—and thus all prefixes 00 through 99 are equally likely—a given ID number is 50 percent more likely to hash into one of the locations 0 through 19 than it is to hash into one of the locations 20 through 39. As a result, each array location 0 through 19 would contain, on average, 50 percent more items than each location 20 through 39.

A function that does not scatter random data evenly

Thus, the hash function h(x) = (first two digits of x) mod 40 does not scatter random data evenly throughout the array table[0..39]. On the other hand, it can be shown that the hash function h(x) = x mod 101 does, in fact, scatter random data evenly throughout the array table[0..100].

A function that does scatter random data evenly

- How well does the hash function scatter nonrandom data? Even if a hash function scatters random data evenly, it may have trouble with nonrandom data. In general, no matter what hash function you select, it is always possible that the data will have some unlucky pattern that will result in uneven scattering. Although there is no way to guarantee that a hash function will scatter all data evenly, you can greatly increase the likelihood of this behavior.

As an example, consider a hash table table[0..99] and a hash function h(x) = first two digits of x. If every ID number is equally likely, h will scatter the search keys evenly throughout the array. But what if every ID number is not equally likely? For instance, a company might assign employee IDs according to department, as follows:

| 10xxxxx | Sales |
| 20xxxxx | Customer Relations |
| ... | ... |
| 90xxxxx | Data Processing |

Under this assignment, only 9 out of the 100 array locations would contain any items at all. Further, those locations corresponding to the largest departments (Sales, for example, which corresponds to table[10]) would contain more items than those locations corresponding to the smallest departments. This scheme certainly does not scatter the data evenly.

Much research has been done into the types of hash functions you should use to guard against various types of patterns in the data. The results of this research are really in the province of more advanced courses, but two general principles can be noted here:

### General requirements of a hash function

- The calculation of the hash function should involve the entire search key. Thus, for example, computing a modulo of the entire ID number is much safer than using only its first two digits.

- If a hash function uses modulo arithmetic, the base should be prime; that is, if h is of the form

```
h(x) = x mod tableSize
```

then tableSize should be a prime number. This selection of tableSize is a safeguard against many subtle kinds of patterns in the data (for example, search keys whose digits are likely to be multiples of one another). Although each application can have its own particular kind of patterns and thus should be analyzed on an individual basis, choosing a prime number for tableSize is an easy way to safeguard against some common types of patterns in the data.
