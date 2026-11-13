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