
# 544 CHAPTER 18 Dictionaries And Their Implementations

![](img/d0cb86b2f18b2db569968ad7c743510e_570_0.png)

> Note: Perspective
> You might wonder why, if the binary search tree implementation of the AD dictionary is so good, we studied the linear implementations at all. There are three reasons. The first and foremost reason is perspective. Section 10.2.4 of Chapter 10 covers the dangers of overanalyzing a problem. If the size of the problem is small, the difference in efficiency among the possible solutions is likely insignificant. In particular, if the size of the dictionary is small, a linear implementation is adequate and simple to understand.
> The second reason is efficiency: A linear implementation can be efficient for certain situations. For example, a linear implementation was best for scenario A, where the predominant operations are insertion and traversal in no order. For scenario B, where the maximum number of items is known, the sorted array-based implementation is adequate, for these situations, a concern for simplicity suggests that you use a linear implementation and not a binary search tree, for large dictionaries.
> The third reason is motivation. By seeing scenarios for which the linear implementations are not adequate, you are free to look beyond and consider other implementations, such as the binary search tree. Actually looking at both a linear implementation and a binary search tree implementation allows you to see these inadequacies more clearly.

![](img/d0cb86b2f18b2db569968ad7c743510e_570_1.png)

## 18.4 Hashing

The binary search tree provides an excellent implementation of the AD dictionary, as the balanced search trees discussed in Chapter 19. They allow you to perform all of the dictionary operations quite efficiently. For example, if a dictionary contains 10,000 items, the operations getItem, add, and remove each require log₁₀(10,000)=4 steps. As this efficiency may be necessary, situations occur for which the search-tree implementations are not adequate.

As you know, time can be vital. For example, when a person calls the 911 emergency system, the system detects the caller's phone number and searches a database of caller information, given a flight number. Locally, an air traffic control system searches a database of flight information, given a flight number. Clearly these searches must be rapid.

A radically different strategy is necessary to locate (insert or remove) an item instantaneously. Imagine an array of Items with each slot capable of holding a single dictionary item—and a seemingly magic box called “address calculator”. Whenever you have a new item to insert into the dictionary, the address calculator will tell you where to place it in the array. Figure 18-9 illustrates this scenario.

You can easily perform an insertion into the dictionary as:

```
add(newItem: Item): boolean

i = index that the address calculator gives you for newItem's search key
table[i] = newItem
```

This addition is O(1); that is, it requires constant time.

You also use the calculator for the getItem and remove operations. If you want to retrieve an item that has a particular key, simply ask the address calculator to tell you where to insert it. Because you would have inserted the item earlier using the add algorithm just, if the desired item is present in the dictionary, it will be in the array location that the address calculator specifies.

## FIGURE 18-9 Address calculator

![](img/d0cb86b2f18b2db569968ad7c743510e_571_0.png)

Thus, the getItem operation appears in pseudocode as follows:

```
getItem(searchKey: KeyType): ItemType throw NotFoundException
 = the array index that the address calculator gives you for an item whose search
key equals searchKey
if table[i].getKey() == searchKey
    return table[i]
else
    Throw NotFoundException
```

Similarly, the pseudocode for the remove operation:

```
remove(searchKey: KeyType): boolean
i = the array index that the address calculator gives you for an item whose search
key equals searchKey
if(table[i].getKey()) == searchKey
{
    Remove the item from table[i]
    isSuccessful = true
}
else
    isSuccessful = false
return isSuccessful
```

It appears that you can perform the operations getItem, add, and remove virtually instantaneously. You never have to search for an item; instead, you simply let the address calculator determine where the item should be. The amount of time required to carry out the operations is O(1) and depends on how quickly the address calculator performs this computation.

If you implement such a scheme, you must be able to construct an address calculator that, with little work, tells you a given item should be. Address calculators are actually not as mysterious as they seem; in fact, there may exist those that approximate the ideal behavior just desired. Such an address calculator is usually referred to as a hash function. The scheme is an ideal description of a technique known as hashing, and the array table is the hash table.

If, to understand how a hash function works, consider the 911 emergency system mentioned earlier. For each person, the system had a record whose search key was the person’s phone number, it could store these records in a search tree. Although searching a tree would be fast, faster access to a particular record would be possible by storing the records in an array table, as follows. You store the record for the...

546 CHAPTER 18 Dictionaries And Their Implementations

> A hash function tells you where to place an item in an array called a hash table

> If fewer than 101 items are present in the hash table table[0..100], it would well tell you to place more than one item into the same array location.

> A hash function maps each search key into an array index

> a unique location of the hash table

> if you know all of the search keys
