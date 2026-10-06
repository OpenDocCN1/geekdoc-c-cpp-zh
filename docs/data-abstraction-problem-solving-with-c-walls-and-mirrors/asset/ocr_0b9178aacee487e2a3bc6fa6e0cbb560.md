# h(4567) = h(7597) = 22

h will tell you to place the two items into the same array, table[22]. That is, the search keys 4567 and 7597 have collided.

Even if the number of items can be in the array at any one time is small, the only way to avoid collisions completely is for the hash table to be large enough that each possible-key value can have its own location. If, for example, Social Security numbers are the search keys, you would need an array location for each integer in the range 0000000099999999. This situation would certainly require a good deal of storage! Reserving vast amounts of storage is usually impractical, collision-resolution schemes are necessary to make hashing feasible. Such schemes usually require that the hash function places items throughout the hash table.

To summarize, a typical hash function

+   * Be easy and fast
* Place items evenly throughout the hash table

Note that the size of the hash table has the ability of the hash function to distribute the items throughout the table. The requirements of a hash function will be discussed in more detail later in this chapter.

Consider several hash functions and collision-resolution schemes.

# 18.4.1 Hash Functions

It is sufficient to consider hash functions that have an arbitrary integer as an argument. If a search key is not an integer, you can simply map the search key into an integer, which you then hash. At the end of this section, you will see one to convert a string into an integer.

Selecting digits. If your search key is the nine-digit employee ID number 001364825, you could select the first digit and the last digit, to obtain 35 as the index to the hash table. That is,

h(001364825) = 35 (select the fourth and last digits)

Therefore, using digit selection to define your hash function, you would store the item search key in 001364825 in table[1]. For example, the first three digits of a Social Security number are based on the geographic region in which you live. If you select only these digits, you will map all people from the same state into the same location of the hash table.

Digit-selection hash functions are simple and fast, but generally they do not evenly distribute the items in the hash table. A hash function should ideally utilize the search key.

Folding. One way to improve the previous approach of selecting digits is to add the digits. The resulting process is known as folding. For example, you can add all the digits in 001364825 to obtain

```
0+0+1+3+6+4+8+2+5 = 29                (the digits)
```

Therefore you would store the item search key is 001364825 in table[29]. Notice that if you add all the digits from a nine-digit search key,

```
0≤h(search key)≤8
```