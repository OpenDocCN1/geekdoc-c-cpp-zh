# 558 CHAPTER 18 Dictionaries and Their Implementations

table[19], while only ID numbers that start with 20 and 60 map into table[20]. In general, three different ID prefixes—that is, the first two digits of an ID number—map into each area 0 through 19, while only two prefixes map into each area 20 through 39. Because all IDs are equally likely—and all prefixes 00 through 99 are equally likely—a given ID number is 50 percent more likely to hash into one of the locations 0 through 19 than it is to hash into that. As a result, each area 0 through 19 would contain, on average, 50 more items than each location 20 through 39.

Thus, the function

```
h(x) = (first two digits of x) mod
```

does not scatter data evenly throughout the array table[0..39]. On the other hand, it can be shown by the hash function

```
h(x) = x mod 101
```

+   As fact, scatter data evenly throughout the array table[0..100].n* How does the hash function scatter nonrandom data? If a hash function scatter random data, it may have trouble with nonrandom data. In general, no matter what hash function you select, it is always possible that the data will have some pattern that result in uneven scattering. There is no way to guarantee that a hash function will scatter all data evenly, you can greatly increase the likelihood of this behavior.

As an example, consider a table[0..39] and a hash function h(x) = two digits of x. If every ID number is equally likely, h will scatter the search keys everythrough out. But what if every ID number is not equally likely? For instance, a company might assign employee IDs to department, as follows:

| 10xxxx | Sales |
| 20xxxx | Customer Relations |

Under this assignment, only 9 out of the 100 array locations would contain any items at all. Further, those locations corresponding to the largest departments (Sales, for example, corresponds to table[10]) would contain more items than those locations corresponding to the smallest departments. This scheme does not scatter the data evenly.

Much research has been done into the types of hash functions you should use to guard against various patterns in the data. The results of this research are relevant in providing advanced courses, but two general principles can be noted here:

+   * The calculation of the hash function should involve the entire search key. For example, computing a modulo of the entire ID number is much safer than using only its first digits.
* If a hash function uses arithmetic, the base should be prime; that is, if h is of the form

```
h(x) = x mod tableSize
```

then tableSize should be a prime number. This selection can safeguard against many subtle patterns in the data (for example, search keys are likely to be multiples of one another). Although each application can have its own kind of patterns and should be analyzed on an individual basis, choosing a prime number for tableSize is an easy way to safeguard against some types of patterns in the data.