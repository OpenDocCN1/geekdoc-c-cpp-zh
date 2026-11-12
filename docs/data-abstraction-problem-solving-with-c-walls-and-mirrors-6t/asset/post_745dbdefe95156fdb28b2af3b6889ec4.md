
### FIGURE 18-13 Double hashing during the insertion of 58, 14, and 91

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_579_0.png)

Because table[3] is occupied, you probe table[10] and find that it, too, is occupied. You finally store 91 in table[(10 + 7) % 11], or table[6].

While more than two hash functions can be desirable, such schemes are difficult to implement.

> Question 7 What is the probe sequence that double hashing uses when h1(key) = key mod 11, h2(key) = 7 - (key mod 7), and key = 19?

Increasing the size of the hash table. With any of the open-addressing schemes, as the hash table fills, the probability of a collision increases. At some point, a larger hash table becomes desirable. If you use a dynamically allocated array for the hash table, you can increase its size whenever the dictionary becomes too full.

You cannot simply double the size of the array, as we did in earlier chapters, because the size of the hash table must remain prime. In addition, you do not simply move the items from the original hash table to the new hash table. If your hash function is x mod tableSize, it changes as tableSize changes. Thus, you need to apply your new hash function to every item in the old hash table before placing it into the new hash table.

> Note: Rehashing After creating a new, larger hash table of an appropriate size, you use the dictionary method add to add each item in the original hash table to the new table. The method computes the hash index using the size of the new table and handles any collisions. This process of enlarging a hash table and computing new hash indices for its contents is called rehashing. You can see that increasing the size of a hash table requires considerably more work than increasing the size of an ordinary array. Rehashing is a task that you should not do often.

- Each hash-table location can accommodate more than one item
- A bucket is an element of a hash table that is itself an array
- Each hash-table location is a linked chain
- Separate chaining successfully resolves collisions

### Approach 2: Restructuring the hash table

Another way to resolve collisions is to change the structure of the array table—the hash table—so that it can accommodate more than one item in the same location. We describe two such ways to alter the hash table.

Buckets. If you define the hash table so that each location table[i] is itself an array—called a bucket—you can store the items that hash into table[i] in this array. The problem with this approach, of course, is choosing the size b of each bucket. If b is too small, you will only have postponed the problem of collisions until b + 1 items map into some array location. If you attempt to make b large enough so that each array location can accommodate the largest number of items that might map into it, you are likely to waste a good deal of storage.

Separate chaining. A better approach than using buckets is to design the hash table as an array of linked chains. In this collision-resolution technique, known as separate chaining, each entry table[i] is a pointer to a chain of linked nodes containing the items that the hash function has mapped into location i, as Figure 18-14 illustrates. Separate chaining provides a successful approach to resolving collisions. With separate chaining, the size of the dictionary is dynamic and can exceed the size of the hash table, because each linked chain can be as long as necessary. As you will see in the next section, the length of these chains affects the efficiency of retrievals and removals. Even so, separate chaining is the most time-efficient collision-resolution scheme.

We will discuss an implementation of the ADT dictionary using hashing and separate chaining in Section 18.4.6 of this chapter.

### FIGURE 18-14 Separate chaining

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_580_0.png)

> Question 8 If h(x) = x mod 7 and separate chaining resolves collisions, what does the hash table look like after the following insertions occur: 8, 10, 24, 15, 32, 177 Assume that each item contains only a search key.

## 18.4.3 The Efficiency of Hashing

An analysis of the average-case efficiency of hashing involves the load factor alpha (α), which is the ratio of the current number of items in the dictionary to the maximum size of the array dictionary. That is,

\(\alpha = \frac{\text{Current number of table items}}{\text{tableSize}}\)

The load factor measures how full a hash table is. $\alpha$ is a measure of how full the hash table is. As the table fills, $\alpha$ increases and the chance of collision increases, so search times increase. Thus, hashing efficiency decreases as $\alpha$ increases.

Unlike the efficiency of earlier dictionary implementations, the efficiency of hashing does not depend solely on the number $n$ of items in the dictionary. While it is true that for a fixed $tableSize$ efficiency decreases as $n$ increases, for a given $n$ you can choose $tableSize$ to increase efficiency. Thus, when determining the size of the hash table, you should estimate the largest possible $n$ and select $tableSize$ so that $\alpha$ is small. As you will see shortly, $\alpha$ should not exceed 2/3.

Hashing efficiency for a particular search also depends on whether the search is successful. An unsuccessful search requires more time in general than a successful search. The following analyses enable a comparison of collision-resolution techniques.

### Unsuccessful searches generally require more time than successful searches

**Linear probing.** For linear probing, the approximate average number of comparisons that a search requires is

$$\frac{1}{2} \left[ 1 + \frac{1}{1 - \alpha} \right]$$ for a successful search, and

$$\frac{1}{2} \left[ 1 + \frac{1}{(1 - \alpha)^2} \right]$$ for an unsuccessful search

### Do not let the hash table get too full

As collisions increase, the probe sequences increase in length, causing increased search times. For example, for a dictionary that is two-thirds full ($\alpha = 2/3$), an average unsuccessful search might require at most five comparisons, or probes, while an average successful search might require at most two comparisons. To maintain efficiency, it is important to prevent the hash table from filling up.

**Quadratic probing and double hashing.** The efficiency of both quadratic probing and double hashing is given by

$$\frac{-\log_e(1 - \alpha)}{\alpha}$$ for a successful search, and

$$\frac{1}{1 - \alpha}$$ for an unsuccessful search

### Open-addressing schemes require a good estimate of the number of insertions and removals

On average, both techniques require fewer comparisons than linear probing. For example, for a dictionary that is two-thirds full, an average unsuccessful search might require at most three comparisons, or probes, while an average successful search might require at most two comparisons. As a result, you can use a smaller hash table for both quadratic probing and double hashing than you can for linear probing. However, because they are open-addressing schemes, all three approaches suffer when you are unable to predict the number of insertions and removals that will occur. If your hash table is too small, it will fill up, and search efficiency will decrease.

**Separate chaining.** Because the dictionary's add operation places the new item at the beginning of a linked chain within the hash table, it is O(1). The getItem and remove operations, however, are not as fast. They each require a search of the linked chain of items, so ideally you would like for these chains to be short.

### Insertion is instantaneous

For separate chaining, $tableSize$ is the number of chains, not the maximum number of dictionary items. Thus, it is entirely possible, and even likely, that the current number of dictionary items $n$ exceeds $tableSize$. That is, the load factor $\alpha$, or $n / tableSize$, can exceed 1. Because $tableSize$ is the number of linked chains, $n / tableSize$—that is, $\alpha$—is the average length of each linked chain.
