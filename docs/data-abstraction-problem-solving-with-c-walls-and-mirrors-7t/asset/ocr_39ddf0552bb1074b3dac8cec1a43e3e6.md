As an alternative to the insert statement, you can use the [ ] operator:

```
myMap['A'] = 100;
myMap['B'] = 200;
myMap['C'] = 300;
```

Other operations for the STL map use a parameter of key_type or an iterator to identify the entry to act upon.

| OPERATION | DESCRIPTION | EFFICIENCY |
| :--- | :--- | :--- |
| void clear() | Destroys all entries in the container and changes its size to 0. | O(n) |
| void insert(pair_type& item) | Inserts item (grows container). | O(log n) |
| uint erase(key_type& item) | Removes all entries matching item from the container (shrinks container). | O(log n) |
| void erase(iterator& position) | Removes the entry at position from the container (shrinks container). | O(1) |
| iterator find(key_type& item) | Returns an iterator referencing item. | O(log n) |
| uint count(key_type& item) | Counts the occurrences of item in the container. For set, this count is at most 1; it can vary for multiset. | O(log n) |
| iterator lower_bound(key_type& item) | Returns an iterator referencing the first entry not less than item. | O(log n) |
| iterator upper_bound(key_type& item) | Returns an iterator referencing the first entry greater than item. | O(log n) |
| iterator begin() | Returns an iterator to the first entry of the container. | O(1) |
| iterator end() | Returns an iterator to the last entry of the container. | O(1) |
| reverse_iterator rbegin() | Returns a reverse iterator to the last entry of the container. | O(1) |
| reverse_iterator rend() | Returns a reverse iterator to the first entry of the container. | O(1) |

As mentioned earlier, the unordered variations of the associative containers are hash-based— they use a hashing function to determine the position of an entry inserted into the container. When you instantiate an unordered associative container, you can use the default hash function for the type of data you are inserting or you can specify your own. Most often, the default hash function will produce acceptable results, but if you are testing your own hashing algorithm, you have the option to pass it to the constructor of an unordered associative container.

Since hash functions are difficult to write, it is often helpful to take advantage of an STL provided hash. The current C++ standard, C11, did not provide a stand-alone hash function. An unordered associative container, typically an unordered_map, must be instantiated first. Then, the hash function for that container can be used to hash any key of the correct type. Section 18.4.1 in Chapter 18 contains a Programming Tip that demonstrates one way to use this hash within the getHashIndex function.

Let's look at a slightly different way of implementing the getHashIndex function in the HashedDictionary class discussed in Chapter 18. We need to take two steps when using the unordered_map hash function within getHashIndex. Instantiate an unordered_map object, and create a variable to represent the hash function. We can accomplish both of these tasks within the header file of HashedDictionary.