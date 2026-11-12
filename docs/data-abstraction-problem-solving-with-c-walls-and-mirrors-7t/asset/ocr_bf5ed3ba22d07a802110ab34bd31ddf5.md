# FIGURE 18-9 Address calculator

![](bbox=[0.185, 0.135, 0.645, 0.285])

Thus, the getItem operation appears in pseudocode as follows:

```
getItem(searchKey: KeyType): ItemType throw NotFoundException
    i = the array index that the address calculator gives you for an item whose search
        key equals searchKey
    if (table[i].getKey() == searchKey)
        return table[i]
    else
        throw NotFoundException
```

Similarly, the pseudocode for the remove operation is

```
remove(searchKey: KeyType): boolean
    i = the array index that the address calculator gives you for an item whose search
        key equals searchKey
    if (table[i].getKey() == searchKey)
    {
        Remove the item from table[i]
        isSuccessful = true
    }
    else
        isSuccessful = false
    return isSuccessful
```

It thus appears that you can perform the operations getItem, add, and remove virtually instantaneously. You never have to search for an item; instead, you simply let the address calculator determine where the item should be. The amount of time required to carry out the operations is O(1) and depends only on how quickly the address calculator can perform this computation.

If you are to implement such a scheme, you must, of course, be able to construct an address calculator that can, with very little work, tell you where a given item should be. Address calculators are actually not as mysterious as they seem; in fact, many exist that can approximate the idealized behavior just described. Such an address calculator is usually referred to as a **hash function**. The scheme just described is an idealized description of a technique known as **hashing**, and the array table is called the **hash table**.

A hash function tells you where to place an item in an array called a hash table.

To understand how a hash function works, consider the 911 emergency system mentioned earlier. If, for each person, the system had a record whose search key was the person's telephone number, it could store these records in a search tree. Although searching a tree would be fast, faster access to a particular record would be possible by storing the records in an array table, as follows. You store the record for a person whose telephone number is t into table[t]. Retrieval of the record, then, is