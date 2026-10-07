# 508 C++ LIBRARY EXTENSIONS (TR1)

```
std::cout << " Bucket " << i << " has " << ht.bucket_size(i) <<
      " elements" << std::endl;
```

```
std::cout << " Hash values" << std::endl;
for(unordered_map<Key, double>::const_iterator iter = ht.begin();
  iter != ht.end(); ++iter)
    std::cout << " was placed in bucket "
      << ht.bucket(iter->first) << std::endl;
```

```
std::cout << " The elements in bucket 0 are " << std::endl;
for(unordered_map<Key, double>::iterator iter = ht.begin(0);
  iter != ht.end(0); ++iter)
    std::cout << " " << iter->first << " ";
std::cout << std::endl;

return0;
```

```
return 0;
}
```

A container with three (initial) buckets that uses hash<Key> functor is created with the defaultdict constructor for the unordered_map<Key, double> class. The maximum load factor is then set to 5. A group of key objects are created and inserted into the table using the overloaded insertion operator. After insertion we check the number of elements and buckets in the table and then determine the number of (Key, double) pair objects that have been placed in each of the buckets.

An iterator is used with a for loop to travel through the table. The Key component of each element in the table is accessed by the iterator and printed along with its bucket number to standard output. First the bucket is examined. This is accomplished using a quantity called local_iterator(or, for containers, const::local_iterator is available) that can define for a specific bucket. In particular, each bucket has a local version of the global begin and end methods that return iterators that are specific to the bucket with index bucketIndex and end(bucketIndex) give iterators.
The output produced by our program is

Size: 9, Number of Buckets: 3
Bucket 0 has 4 elements
Bucket 1 has 2 elements
Bucket 2 has 3 elements

Hash values
(s6,7) was placed in bucket 0
(s4,5) was placed in bucket 0
(s3,4) was placed in bucket 0
(s1,2) was placed in bucket 0
(s9,10) was placed in bucket 1
(s2,3) was placed in bucket 1
(s8,9) was placed in bucket 2
(s7,8) was placed in bucket 2
(s5,6) was placed in bucket 2
The elements in bucket 0 are
(s6,7) (s4,5) (s3,4), (s1,2)

By setting the maximum load factor sufficiently, we have made that the table would not be expanded by the two buckets requested from the constructor. The first (index 0) bucket is the one with the most elements and these are examined in both the global and local exploration of the container.