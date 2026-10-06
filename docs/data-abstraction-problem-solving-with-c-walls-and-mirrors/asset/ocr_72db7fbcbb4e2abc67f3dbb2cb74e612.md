# 546 CHAPTER 18

# Dictionaries and Their Implementations

almost instantaneous given its search key t. For example, you can store the record for the telephone 123-4567 in table[1234567]. If you can spare 10 million locations for table,1, this approach is fine. You need not use memory so extravagantly, however, because 911 systems are regional. If you use only one telephone exchange, for example, you can store the record for the 123-4567 in table[e4567] and get it by an array table of 10,000 locations.

The transformation of 1234567 into an array 4567 is a simple example of a hash function. A hash function must take an index x and map it into an integer that you can use as an array index. Such indices would be in the range 0 through 9999. That is, h is a function for any integer x,

```
h(x) = i, where i is an integer in the range 0 through 9999
```

Because the database contains every telephone number in a particular exchange, the array table is completely full. In this, our example is not typical of hashing applications and serves only to illustrate the idea of a hash function. What if we, an air traffic control system stores an entry for each flight accord for its four-digit flight number? You could store an entry for Flight 4567 in table[e4567] but would still need an array of 10,000 locations, even if only 50 flights were.

A different hash function would save memory. If you allow space for a maximum of 101 flights, for example, so that the array table has 0 through 100, the necessary hash function h would map any four-digit flight number into an integer in the range 0 through 100.

If you have such a hash function h—and you will see several suggestions for hash functions the dictionary operations are easy to write. For example, the getTree algorithm, the

```
i = the array index that the calculator gives you for an item we search keys search
```

is implemented by

```
i = h(searchKey)
```

In the previous example, searchKey would be the flight number.

Although the dictionary operations appear to be virtually instantaneous, hashing is really as good as it sounds? If it were that good, there would have little reason for developing all other dictionary implementations. Hashing would beat them hands down!

Why is not as simple as it seems? When you notice that the hashing scheme stores the items in an array, it would appear to suffer from the familiar problems associated with a fixed-size implementation. Obviously, the hash table must be large enough to contain all of the items you want to store. This isn is not the result of the implementation's difficulty, however, for—as you will see later—there are ways to allow the hash table to grow dynamically. But the number of items to store will never exceed the size of the hash table

We want the hash function to map each search key x into an integer i. The hash function in the ideal situation is a perfect hash function. In fact, it is possible to construct perfect hash functions if you know all of the possible search keys that actually occur in the dictionary. You have for the 911 example, where everyone is in the database, but not for the traffic control system. Usually, you will not know the values of the search keys in advance.

In practice, a hash function may store two or more search keys x and y into the same integer. That is, the hash function allows you to store two or more items in the same array location table[1]. This occurrence is called a collision. Even if fewer than 101 items are present in the hash table table[0..100], it would well tell you to place more than one item into the same array location. For example, if two items have search keys 4567 and 7597, and if

A hash function maps each search key into an array index

a unique location of the hash table

if you know all of the search keys