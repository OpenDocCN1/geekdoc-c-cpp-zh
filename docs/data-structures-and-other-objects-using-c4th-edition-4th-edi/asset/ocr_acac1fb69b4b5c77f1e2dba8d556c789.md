In this case, we can store the records in an array called data with only 50 components. The record with stock number i can be stored at this location:

```
data[i / 100]
```

With the aid of integer division, we can make do with the indexes 0 through 49, even though the numbers become as large as 4900. If we want stock number 700, we compute 700/100 and obtain the index 7. The record for stock number 700 is stored in array component data[7].

# hash function

This general technique is called hashing. Each record requires a unique identifying value called its key. In our example, the key was the stock number stored in a member variable called key, but other, more complex keys are sometimes used. A function, called the hash function, maps key values to array indexes. Suppose we name our hash function hash. If record has a key value of i, then we will try to store that record at location data[hash(i)]. Using the hash function to compute the correct array index is called hashing the key to an array index. The hash function must be chosen so that its return value is always a valid index for the array. The hash function may be either a declared C++ function or a simple arithmetic expression. In our example, hash(i) was this expression:

```
i / 100
```

# collisions

In our example, every key produced a different index value when it was hashed. That is a perfect hash function, but unfortunately a perfect hash function cannot always be found. Suppose we change the example so that we no longer have stock number 400, but we have 399 instead. Then the record with stock number 300 will be placed in data[3] as before, but where will stock number 399 be placed? Stock number 399 is supposed to be placed in data[399/100]. In other words, the record for stock number 399 is supposed to be placed in data[3]. There are now two different records that belong to data[3]. This situation is known as a collision. In this case we could redefine the hash function to avoid the collision. But in practice, you do not know the exact numbers that will occur as keys, and therefore you cannot design a hash function that is guaranteed to be free of collisions (unless, perhaps, your insider at the tractor company has a lot of pull). Something must be done to cope with the tractor collisions.

Typically you do not know what numbers will be used as the key values, but you do know an upper bound on how many there will be. The usual approach is to use an array size that is larger than needed—later we will see formulas that indicate how many extra positions are needed. The extra array positions make collisions less likely. A good hash function will distribute the key values uniformly through the index range of the array. If the array indexes range from 0 to 99, then you might use the following hash function to produce an array index for a record with a given key:

```
key % 100
```