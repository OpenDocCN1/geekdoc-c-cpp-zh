
## 9.4 Hashing

with key $k$ can be stored in $HT[k]$, and the hash function is simply $h(k) = k$. To find the record with value key $k$, simply look in $HT[k]$.

Typically, there are many more values in the range than there are slots in the hash table. Given a realistic example, suppose that the key can take some value in the range 0 to 65,535 (i.e., the key is a two-byte unsigned integer), and that we expect to store approximately 1000 records at any given time. It is impractical in this situation to use a hash table with 65,536 slots, because most of the slots will be left empty. Instead, we must devise a hash function that allows us to store the records in a much smaller table. Because the possible key range is larger than the size of the table, at least some of the slots must be mapped to multiple key values. Given a hash function $h$ and two keys $k_1$ and $k_2$, if $h(k_1) = \beta = h(k_2)$ where $\beta$ is a slot in the table, then we say that $k_1$ and $k_2$ have a collision at slot $\beta$ under function $h$.

Finding a record with value key $K$ in a database organized by hashing follows a two-step procedure:

1. Compute the table location $h(K)$.
2. Starting with $h(K)$, locate the record containing $K$ using (if necessary) **collision resolution policy**.

### 9.4.1 Hash Functions

Hashing generally takes records whose values come from a large range and stores them in records with a relatively small number of slots. Collisions occur when two records hash to the same slot in the table. If we are careful—lucky—selecting a hash function, the actual number of collisions will be nearly unavoidable. For example, consider a classroom of students. What is the probability that some students share the same birthday (i.e., the same day of the year, not necessarily the same year)? If there are 23 students, the odds are about that two will share a birthday. This is despite the fact that there are 365 days in which students can have birthdays (ignoring leap years), most no student in the class has a birthday. The mapping of students to days based on their birthday is similar to assigning records to a table (of size 365) using the birthday as a hash function. Note that this observation tells us nothing about which students share a birthday, or on which days of the year shared birthdays falls.

> Exception to this is perfect hashing. Perfect hashing is a system in which records are hashed such that there are no collisions. A hash function is selected for the specific set of records being hashed, which requires the entire collection of records to be available before selecting the hash function. Perfect hashing is efficient because it always finds the record that we are looking for exactly where the hash function computes it, so only one access is required. Selecting a perfect hash function can be expensive, but might be worthwhile when extremely efficient search performance is required. An example is searching for data on a read-only CD. Here the database will never change, the time for each access is expensive, and the database designer can design the hash table before issuing the CD.

To be practical, a database organized by hashing must store records in a hash table that is not so large that it wastes space. Typically, this means that the hash table will be around half full. Because collisions are extremely likely to occur under these conditions (by chance, any record inserted into a table that is half full with a collision half of the time), does this mean we do not need to worry about the ability of a hash function to avoid collisions? Absolutely. Not the difference between a good hash function and a bad hash function makes a big difference in practice. Technically, any function that maps all possible key values to a slot in the table is a hash function. In the extreme case, even a function that maps all records to the same slot is a hash function, but it does nothing to help us find records during a search operation.

each slot in the table has equal probability of being filled. Unfortunately, we have no control over the key values of the actual records, so well any particular hash function depends on the distribution of the keys within the allowable range. In some cases, incoming data are well distributed across their key range. For example, if the input is a set of random numbers selected uniformly from the key range, any hash function assigns the key so that each slot in the hash table receives an equal share of the range will likely also distribute the incoming records uniformly within the table. However, in many applications the incoming records are highly clustered or otherwise poorly distributed. When input records are not well distributed throughout the range it can be difficult to define a hash function that does a good job of distributing the records throughout the table, especially if the input distribution is not known in advance.

There are many reasons why data values might be poorly distributed.

1. Natural frequency distributions tend to follow a pattern where a few of the entities occur frequently while most entities occur relatively rarely. For example, consider the populations of the 100 largest cities in the United States. If you plot these populations on a number line, most of them will be clustered towards the low side, with a few outliers on the high side. This is an example of a Zipf distribution (see Section 9.2). Viewed the other way, the home for a given person is far more likely to be a particular large city than a small town.
2. Collected data are likely to be skewed in some way. Field samples might be rounded to, say, the nearest 5 (i.e., all numbers end in 5 or 0).
3. If the input is a collection of common English words, the beginning letter will be poorly distributed.

## Sec. 9.4 Hashing

Note that in examples 2 and 3, either high- or low-order bits of the key are poorly distributed.

When designing hash functions, we are generally faced with one of two situations.

1. We know nothing about the distribution of the incoming keys. In this case, we wish to select a hash function that evenly distributes the key range across the hash table, while avoiding obvious opportunities for clustering as hash functions that are sensitive to the high- or low-order bits of the key value.
2. We know something about the distribution of the incoming keys. In this case, we should use a distribution-dependent hash function that assigns clusters of related keys to the same hash table slot. For example, if hashing English words, we should *not* hash on the value of the first character because this is likely to be unevenly.

Below are several examples of hash functions that illustrate these points.

**Example 5** Consider the hash function used to hash integers to sixteen slots:

```
int h(int x) {
  return x % 16;
}
```

The value returned by this hash function depends solely on the least significant bits of the key. Because these bits are likely to be poorly distributed (an example, a high percentage of the keys might be even numbers, which means that the low bit is zero), the result will also be poorly distributed. This example shows that the size of the table $M$ can have a big effect on the performance of a hash system because this is typically used as the modulus to ensure that the hash function produces a number in the range $0$ to $M-1$.

**Example 9.6** A good hash function for numerical values comes from the mid-square method. The mid-square method squares the key value, and then takes the $r$ bits of the result, giving a value in the range $0$ to $2^r-1$. This works well for most or all of the key value contribute to the result. For example, consider whose whose keys are 4-digit numbers in base 10. The goal is to hash these keys to a table of size 100 (i.e., a range of $0$ to $99$). This range is equivalent to two digits in base 10. That is, $r=2$. If the input is the number 4567, squaring yields an 8-digit number, $20857489$. The middle two digits of this result are 57. All digits
