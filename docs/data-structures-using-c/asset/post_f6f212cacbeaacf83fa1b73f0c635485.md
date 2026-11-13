
with two keys, both the records are stored in the same bucket. The assumption is that the buckets are equal in size.

Consider the following example. Suppose we want to store 5 records with the key of each record as the person's name. The key can be hashed by taking the address from the ASCII representations of the first characters of the name. The table is of size 26, i.e., one bucket for each alphabet with size 2 (Table 11.2a) or size 3 (Table 11.2b).

**Table 11.2(a) Table with bucket size 2**

| Index | | |
| :--- | :--- | :--- |
| 0 | Alka | Abhay |
| 1 | Bindu | Babali |
| 2 | | |
| 3 | Deepa | Deven |
| 4 | Ekta | Esha |
| 5 | | |
| 6 | Govind | Gopal |
| : | : | : |
| 13 | Monika | Meera |
| : | : | : |
| 18 | Sharmila | Sindhu |
| : | : | : |
| 25 | Zinat | Ziya |

**Table 11.2(b) Table with bucket size 3**

| Index | | | |
| :--- | :--- | :--- | :--- |
| 0 | Alka | Abhay | Asmita |
| 1 | Bindu | Babali | Bhanu |
| 2 | | | |
| 3 | Deepa | Deven | Deepak |
| 4 | Ekta | Esha | Eshwar |
| 5 | | | |
| 6 | Govind | Gopal | Gautam |
| : | : | : | : |
| 13 | Monika | Meera | Manisha |
| : | : | : | : |
| 18 | Sharmila | Sindhu | Shilpi |
| : | : | : | : |
| 25 | Zinat | Ziya | Zeba |

**Probe** Each action of address calculation and check for success is called as a *probe*.

**Collision** The result of two keys hashing into the same address is called collision.

**Synonym** Keys that hash to the same address are called synonyms.

**Overflow** The result of many keys hashing to a single address and lack of room in the bucket is known as an overflow. Collision and overflow are synonymous when the bucket is of size 1.

**Open or external hashing** When we allow records to be stored in potentially unlimited space, it is called as *open or external hashing*.

**Closed or internal hashing** When we use fixed space for storage eventually limiting the number of records to be stored, it is called as *closed or internal hashing*.

**Hash function** Hash function is an arithmetic function that transforms a key into an address which is used for storing and retrieving a record.

**Perfect hash function** The hash function that transforms different keys into different addresses is called a *perfect hash function*. The worth of a hash function depends on how well it avoids collision.

**Load density** The maximum storage capacity, that is, the maximum number of records that can be accommodated, is called as *loading density*.

**Full table** A full table is one in which all locations are occupied. Owing to the characteristics of hash functions, there are always empty locations, rather a hash function should not allow the table to get filled in more than 75%.

**Load factor** Load factor is the number of records stored in a table divided by the maximum capacity of the table, expressed in terms of percentage.

**Rehashing** Rehashing is with respect to closed hashing. When we try to store a record with Key1 at the bucket position Hash(Key1) and find that it already holds a record, it is collision situation. To handle collision, we use a strategy to choose a sequence of alternative locations Hash1(Key1), Hash2(Key1), and so on within the bucket table so as to place the record with Key1. This is known as *rehashing*.

**Issues in hashing** In case of collision, there are two main issues to be considered:

- 1. We need a good hashing function that minimizes the number of collisions.
- 2. We want an efficient collision resolution strategy so as to store or locate synonyms.

Let us learn about these two issues and techniques to resolve them in Sections 11.3 and 11.4, respectively.

## 11.3 HASH FUNCTIONS

To store a record in a hash table, a hash function is applied to the key of the record being stored, returning an index within the range of the hash table. The record is stored at that index position, if it is empty. With direct addressing, a record with key K is stored in slot K. With hashing, this record is stored at the location Hash(K), where Hash(K) is the function. The hash function Hash(K) is used to compute the slot for the key K. Let us discuss some issues regarding the design of good hash functions and also study the schemes for their creation.

### 11.3.1 Good Hash Function

The average performance of hashing depends on how the hash function distributes the set of keys among the slots. An assumption is that any given record is equally likely to hash into any of the slots, independent of whether any other record has been already hashed to it or not. This assumption is known as *simple uniform hashing*. A good hash function is one which satisfies this assumption.

If the probability that a key 'Key' occurs in our collection is P(Key), and for M slots in our hash table, a uniform hashing function, Hash(Key), should ensure that for $0 \le \text{Key} \le M-1$, $\Sigma P(\text{Key}) = 1$, are all equiprobable with probability 1/M. The hash function should ensure that they are hashed to different locations.

Sometimes, this is easy to ensure. For example, if the keys are randomly distributed in [0 .. r], with 0 to M – 1 locations then, Hash(Key) = floor((M × Key)/r) will provide uniform hashing.

### Features of a Good Hashing Function

- 1. Addresses generated from the key are uniformly and randomly distributed.
- 2. Small variations in the value of the key will cause large variations in the record addresses to distribute records (with similar keys) evenly.
- 3. The hashing function must minimize the occurrence of collision.

There are many methods of implementing hash functions, let us discuss a few of them.

### 11.3.2 Division Method

One of the required features of the hash function is that the resultant index must be within the table index range. One simple choice for a hash function is to use the modulus division indicated as MOD (the operator % in C/C++). The function MOD returns the remainder when the first parameter is divided by the second parameter. The result is negative only if the first parameter is negative and the parameters must be integers. The function returns an integer. If any parameter is NULL, the result is NULL.

```
Hash(Key) = Key % M
```

Key is divided by some number M, and the remainder is used as the hash address. This function gives the bucket addresses in the range of 0 through (M – 1), so the hash table should at least be of size M. The choice of M is critical. While using this method, we usually avoid certain values of M. Binary keys of length in powers of two are usually avoided. A good choice of M is that it should be a prime number greater than 20.

### 11.3.3 Multiplication Method

Another hash function that has been widely used in many applications is the multiplication method. The multiplication method works as follows:

- 1. Multiply the key 'Key' by a constant A in the range 0 < A < 1 and extract the fractional part of Key × A.
- 2. Then multiply this value by M and take the floor of the result.

```
Hash(Key) = ⌊M × ((Key × A) MOD 1)⌋,
```

where Key × A MOD 1 is the fractional part of Key × A, that is, Key × A – ⌊Key × A⌋ and one of the commonly used values of A = (sqrt(5) – 1)/2 = 0.6180339887.

An advantage of the multiplication method is that the value of M is not critical. We typically choose it M = 2^p for some integer p, since we can then easily implement the function in any programming language as:

- 1. Choose \( M = 2^p \).
- 2. Multiply the \( \omega \) bits of Key by floor \( (A \times 2\omega) \) to obtain a \( 2\omega \) bit product.
- 3. Extract the \( p \) most significant bits of the lower half of this product as address.

Note that we have used the functions floor and ceil are the commonly used math functions available in the library of almost all programming languages. These functions map a real number to the largest preceding or the smallest following integer, respectively. More precisely, floor(x) = \( \lfloor x \rfloor \) is the largest integer not greater than x and ceil(x) = \( \lceil x \rceil \) is the smallest integer not less than x.

### 11.3.4 Extraction Method

When a portion of the key is used for address calculation, the technique is called as the extraction method. In digit extraction, a few digits are selected, extracted from the key and are used as the address. For example, if the book accession number is of six digits and we require an address of 3 digits, then we can select the odd number digits—first, third, and fifth—which can be used as the address for the hash table.

| Key | Hashed address |
|---|---|
| 345678 | 357 |
| 234137 | 243 |
| 952671 | 927 |

For example, Table 11.3 shows the keys with their respective hashed addresses using digit extraction. Another way is to extract the first two and the last one or two digits. For example, for key 345678, the address is 3478 if the first two and the last two digits are extracted or 348 if the first two and the last digit are extracted.

If the portion of the key is carefully selected, it can be sufficient for hashing, provided the remaining portion distinguishes the keys in an insufficient way.

### 11.3.5 Mid-square Hashing

Mid-square hashing suggests to take the square of the key and extract the middle digits of the squared key as the address. The difficulty is when the key is large. As the entire key participates in the address calculation, if the key is large, then it is very difficult to store its square as it should not exceed the storage limit. So mid-square is used when the key size is less than or equal to 4 digits. For example, Table 11.4 shows the keys with their hashed addresses. If the key is a string, it has to be preprocessed to produce a number.

| Key | Square | Hashed address |
|---|---|---|
| 2341 | 5480281 | 802 |
| 1671 | 2792241 | 922 |
