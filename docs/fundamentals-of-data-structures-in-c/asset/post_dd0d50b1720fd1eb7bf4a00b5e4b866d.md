
| Unsorted List | 56 | 91 | 35 | | 72 | 48 | 68 |
|---|---|---|---|---|---|---|---|
| | 56 | 91 | 35 | | 72 | 48 | 68 |
| | 35 | 91 | 56 | | 72 | 48 | 68 |
| | 35 | 72 | 56 | 91 | 48 | 48 | 68 |
| | 35 | 72 | 56 | 48 | 91 | 91 | 68 |
| | 35 | 72 | 56 | 48 | 68 | 68 | 91 |
| | 35 | 68 | 56 | 48 | 72 | 72 | 91 |
| | 35 | 56 | 68 | 48 | 48 | 72 | 91 |
| | 35 | 56 | 48 | 48 | 68 | 72 | 91 |
| Sorted List | 35 | 48 | 56 | 68 | 72 | 91 |

## Fig. 5.4 : Trace of a quick sort.

The pivot selected should be such that it is smaller than about half the elements and larger than about half the elements. Consider the extreme case where either the smallest or the largest value is chosen as the pivot. When quick sort is called recursively on the values on either side of it, one set of data will be empty while the other would be almost as large as the original data set. If a bad pivot element is chosen, the array will not be evenly divided and quick sort may be called on an array that is just as big as the original array.

In the best case, quick sort is said to be O(n log n) and this case occurs when the input array is evenly divided. In the worst case, the timing of the quick sort is O(n^2). This case occurs when the pivot element fails to divide the input array at all (i.e., all elements are greater than or smaller than the pivot element). To improve the efficiency of the sort, there are clever ways to choose the pivot value such that it is extremely unlikely to end up with an extreme value. One such method is called the median-of-three partitioning. In this method, three elements are randomly chosen and the median of these three values is chosen as the pivot element.

## 5.8 Hashing

Hashing is a data structure that allows insertion, deletion and search operations to be carried out in O(1) time. However, hashing is not efficient in operation that requires any ordering information among the elements, such as sorting, finding minimum and maximum element.

Let us assume we need to keep information about 500 students. Hence, we can assign an identification number to each student between 0 and 499 and then use a multidimensional array of 500 elements. Accessing elements in an array is extremely efficient. Array elements are usually accessed by index (also referred as its subscript). To search for a particular record, we have to search the whole array sequentially till we find the required record. Hence, the search time to find a particular data item in the array is proportional to the number of data items in the list, since the item to be searched may be at the first position, any intermediate position or at the last position. Similarly, if we want to store Reg_No (which is supposed to be an 11-digit number) of each student in an array, if we want to directly use the Reg_No as an index, the table should have much more elements than the number of the students, which is a great waste of space. The modern approach is that to make the entries in the table in sorted order of the primary key. Then we apply any of the sorting and searching techniques to get the desired record, which reduces the search time considerably. But the movement of existing records of the table in sorted order is unnecessary and it is a difficult task. To overcome this problem, we generate a table for the records in the file. Then we take the primary key of each record, and apply a function to manipulate it and generate an address value and store the record, at the generated address. Hence, if we map the 500 Reg_Nos of the students and the numbers between 0-499, then we can use the Reg_No as search keys and still use an array of 500 elements to store the records. If we can find a mapping between the search keys and indices, we can store each record in the element with the corresponding index. Thus each element would be found with one operation only, such a technique is referred to as *hash addressing* or *hashing*.

This hashing technique is used in searching for a particular record in a file. So we will use the concept of files to analyze this technique. Let us assume a file F having N records. This file has a set of fields SF that forms the primary key PK of the file (i.e., *Roll_No* field in the students record is unique for every student in the college). This primary key PK is used to uniquely identify a particular record in a file. We assume that this file is maintained by a table kept in memory, which stores the primary key PK and the address part of the record with the primary key PK, which directly refers records in a table by doing arithmetic operations on keys to map them onto the respective table addresses. Such a table which maintains the key (of the item that is mapped to an index value) is referred to as the *hash table*. The hash table is sometimes referred to as *scatter table*, because we are trying to scatter the data throughout the table. Each slot in the array (which is considered as a hash table) is sometimes referred to as a *bucket*.

A hash table is a data structure that works just like an array, except instead of forcing you to use integers as your index you can use any arbitrary data type as your index. Basically a function is needed to map a key K to an integer index i of the hash table (which has indices 0 to n), such a function is referred as the *hashing function*. Ideally, the hash function is used to determine the location (table index) of any record, given its key value.

Hash functions transform the keys into numbers within a predetermined interval (0 to n). These numbers are then used as indices in an array in the hash table to store the records. If the indices are numbers and if N is the size of the array, then h(key) = key % N. This will map all the keys into numbers within the interval (0 to n-1). If the indices are strings of characters, treat the binary representation of a key as a number and then apply the string as before. If each character is represented with m bits, then the string can be treated as base-m number.

We should choose a hash function such that it gives us distinct values for different values of primary key. Unfortunately, sometimes, two different values may hash to the same address. This situation, where two different key values hash to the same hash address, is referred to as *collision*.

In this collision condition for inserting the new pair, another possible location has to be found. And if all the buckets are filled then this condition is called *overflow*. So, we should have some resolution methods to avoid such overflow.

- The methods for handling overflow are
  - Open addressing
  - Chaining.

The integer, generated by a hash function between 0 and N-1 is used as an index in a hash table of n elements. Initially all slots in the hash table are blank. To insert values into the hash table, use the hash function to generate an address for each value to be inserted. To search for a key in the table the same hash function is reused. An important consideration in hashing performance is value of the *load factor*, which is denoted by (λ) and is defined as the ratio between the number of records to be stored and the size of the table. As the load factor increases, the hashing performance will degrade because of the time required to search collision chains.

The value that the hash function returns for a given key is its hash address. A perfect hash function maps every key into a different table location. It has been proved that if P is a prime number, we obtain better (more even) distribution of the keys over the table. The key obtained by transforming the string into a number using the modulus operation utilizes most of the information in the string. We can use different methods to generate an address from the key value in hash function. Some methods of importance are,

- Truncation method
- Folding method
- Mid-square method
- Division method.

## 5.8.1 Truncation Method.

Truncation method is the simplest and easiest method for computing keys using the hash function. Let us consider that you want to generate hash table address for the following keys,

- 987456 125978 963294 852137

The truncation method truncates a part of the given keys, depending upon the size of the hash table. If we assume that the size of the hash table is 1000, then the rightmost (or
