almost instantaneous given its search key t. For example, you can store the record for the telephone number 123-4567 in table[1234567]. If you can spare 10 million memory locations for table1, this approach is fine. You need not use memory so extravagantly, however, because 911 systems are regional. If you consider only one telephone exchange, for example, you can store the record for the number 123-4567 in table[4567] and get by with an array table1 of 10,000 locations.

The transformation of 1234567 into an array index 4567 is a simple example of a hash function. A hash function h must take an arbitrary integer x and map it into an integer that you can use as an array index. In our example, such indices would be in the range 0 through 9999. That is, h is a function such that for any integer x,

```
h(x) = i, where i is an integer in the range 0 through 9999
```

A hash function maps an integer into an array index

Because the database contains entries for every telephone number in a particular exchange, the array table1 is completely full. In this sense, our example is not typical of hashing applications and serves only to illustrate the idea of a hash function. What if many fewer entries were in the array? Consider, for example, an air traffic control system that stores an entry for each current flight according to its four-digit flight number. You could store an entry for Flight 4567 in table1[4567], but you still would need an array of 10,000 locations, even if only 50 flights were current.

A different hash function would save memory. If you allow space for a maximum of 101 flights, for example, so that the array table1 has indices 0 through 100, the necessary hash function h should map any four-digit flight number into an integer in the range 0 through 100.

If you have such a hash function h—and you will see several suggestions for hash functions later—the dictionary operations are easy to write. For example, in the getItem algorithm, the step

```
i = the array index that the address calculator gives you for an item whose search key equals searchKey
```

is implemented simply as

```
i = h(searchKey)
```

In the previous example, searchKey would be the flight number.

Although the dictionary operations appear to be virtually instantaneous, is hashing really as good as it sounds? If it really was this good, there would have been little reason for developing all those other dictionary implementations. Hashing would beat them hands down!

Why is hashing not quite as simple as it seems? You might first notice that since the hashing scheme stores the items in an array, it would appear to suffer from the familiar problems associated with a fixed-size implementation. Obviously, the hash table must be large enough to contain all of the items that you want to store. This requirement is not the crux of the implementation's difficulty, however, for—as you will see later—there are ways to allow the hash table to grow dynamically. But the implementation does have a major pitfall, even given the assumption that the number of items to be stored will never exceed the size of the hash table.

A perfect hash function maps each search key into a unique location of the hash table

Ideally, you want the hash function to map each search key x into a unique integer i. The hash function in the ideal situation is called a perfect hash function. In fact, it is possible to construct perfect hash functions if you know all of the possible search keys that actually occur in the dictionary. You have this knowledge for the 911 example, since everyone is in the database, but not for the air traffic control example. Usually, you will not know the values of the search keys in advance.

A perfect hash function is possible if you know all the search keys

In practice, a hash function can map two or more search keys x and y into the same integer. That is, the hash function tells you to store two or more items in the same array location table1[i]. This occurrence is called a collision. Thus, even if fewer than 101 items were present in the hash table table1[0 .. 100], h could very well tell you to place more than one item into the same array location. For example, if two items have search keys 4567 and 7597, and if