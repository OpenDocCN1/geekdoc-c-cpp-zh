
- 10. Programmers tend to use a struct only when all the members are public.

- 11. Collisions are resolved by placing the item in the next open spot of the array.

- 12. Here's the body of the implementation:

```cpp
{
bool found;
std::size_t index;
assert(key >= 0);
find_index(key, found, index);
return found;
}
```

- 13. Here's the body of the implementation:

```cpp
{
std::size_t index;
assert(key >= 0);
find_index(key, found, index);
if (found)
    result = data[index];
}
```

- 14. Here is the never_used member function:

```cpp
template <class RecordType>
inline bool Table<RecordType>::
never_used(size_t index) const
// Library facilities used: stdlib.h
// Precondition: index < CAPACITY.
// Postcondition: if data[index] has never
// been used, then the return value is true.
// Otherwise the return value is false.
{
    return
    (data[index].key == NEVER_USED);
}
```

Here is the is_vacant member function:

```cpp
template <class RecordType>
inline bool Table<RecordType>::
is_vacant(size_t index) const
// Library facilities used: stdlib.h
// Precondition: index < CAPACITY.
// Postcondition: If data[index] is not now
// being used, then the return value is true.
// Otherwise the return value is false.
{
    return
    (data[index].key < 0);
}
```

- 15. If the key was already present, then the record with that key is overwritten. If the key was not already present, then the assertion tests whether size() < CAPACITY is true, and this assertion fails, halting the program.

- 16. Suppose we start looking in the data array at some index, say 34, and we move forward until we find an unoccupied location. Perhaps this first unoccupied location is at index 36. If position 36 has a key of NEVER_USED, then that indicates that the position has never been used, and therefore no record with the given key appears in the array (since it would have been placed in this unused position, or perhaps in position 34 or 35, which we already examined).

On the other hand, if position 36 has a key of PREVIOUSLY_USED, then this position has previously been used and since removed. In this case, it is possible that there is a record with the given key in the array at a position after data[36]. It might be at this position, because at the time it was inserted, data[36] might have been in use.

- 17. Linear probing can result in clustering of elements when several different keys are hashed to the same location. Insertions and searching take longer as clustering gets worse. Double hashing can solve this problem by using a second hash function to resolve a collision.

- 18. For linear probing, the key/index pairs are 103 at [0], 0 at [1], 205 at [102], 308 at [2], 411 at [3], and 2 at [4]. For double hashing the key/index pairs are 103 at [0], 0 at [1], 205 at [102], 308 at [5], 411 at [7], and 2 at [2].

- 19. There is a twin prime pair at 1229 and 1231, which suggests that 1231 is a good table capacity.

- 20. NULL

- 21. We suggest that you first write a helper function with one parameter that is a key. The function returns a pointer to a node with the specified key (or returns NULL if there is no such node). Using this function (which we call find_ptr), the implementation is:

```cpp
template <class RecordType>
void Table<RecordType>::
insert(const RecordType& entry)
{
    main_savitch_6B::node<RecordType>
    *cursor;

    cursor = find_ptr(entry.key);
    if (cursor == NULL)
    {
        list_head_insert
        (data[hash(entry.key)], entry);
        ++used;
    }
    else
        cursor->set_data(entry);
}
```

- 22. The data[0] list will have the keys 0 and 811. The data[1] list will have the keys 1623. The data[2] list will have the keys 2 and 2435. The data[3] list will have the key 3247. All other lists are empty.

- 23. The ADT does use dynamic memory (the linked lists).

- 24. If the lists are kept in order, then a search can stop as soon as it reaches a key that is greater than the target.

- 25. The load factor is 0.9 (i.e. 180/200). With linear probing, the expected average is 5.50; with double hashing, the expected average is 2.56; with chained hashing, the expected average is 1.45.

- 26. For linear probing, we need a load factor of 2/3, which requires a table capacity of 1500. For double hashing, we need a load factor of just less than 0.8, requiring a table capacity of about 1250. For chaining, we need a load factor of 2, requiring an array size of 500.

- 27. A template parameter can be a data type, a constant data value, or a function.

- 28. Here is one implementation:

```cpp
int hashkey(const string& s)
{
    int result = 0;

    for (int i = 0; i < s.length(); ++i)
        result = result + static_cast<int>(s[i]);

    return (result % table_size);
}
```

- 29. Here is one implementation:

```cpp
bool table::is_present(int key) const
{
    size_t i = hash(key); // If key exists, it will be in data[i].
    vector<RecordType>::const_iterator it;

    for (it = data[i].begin(); it != data[i].end(); ++it)
    {
        if (hashkey(*it) == key)
            return true;
    }

    return false;
}
```

- 30. A copy constructor, destructor, and assignment operator are needed only when a class makes direct use of dynamic memory. The new table class uses dynamic memory, but only through the vector class, which is another great reason to use the STL classes.

## PROGRAMMING PROJECTS

For more in-depth projects, please see www.cs.colorado.edu/~main/projects/

- 1. Reimplement the binary search using a loop and no recursion. If you are familiar with template functions, then your implementation should be a template function that can search any array that is sorted from smallest to largest (using the < operator).

- 2. Use a binary search technique to rewrite the guess_game function from Figure 14.1 on page 24. The function may ask questions such as “Is your number bigger than 42?” Your result should have worst-case time of O(log n).

- 3. Use double hashing to reimplement the hash table from Figure 12.4 on page 604.

- 4. In our open-address hash tables, we have used linear probing or double hashing. Another probing method, which avoids some clustering, is called quadratic probing. The simplest version of quadratic probing works like this: Start by hashing the key to an array index. If there is a collision, then move to the next array index. If there is a second collision, then move forward two more spots through the array. After a third collision, we move forward three more spots, and so on. For example, suppose that a new key hashes to location 327, and this location is full. The next location that we try is 328. If 328 is a second collision, then we move two spots forward to location 330. If 330 is a third collision, then we move three spots forward to location 333. If our calculation of the next spot takes us beyond the end of the array, then we “wrap around” to the front of the array. In general, if data[i] is the location that has just caused a collision, and we have already examined collision elements, then we increase i according to the assignment:

```cpp
i = (i + count) % CAPACITY;
```

In this formula, the “% CAPACITY” causes the “wraparound” to the front of the array. In order for this approach to work correctly, the capacity must be a power of 2, such as 2^10 = 1024. Otherwise, the sequence of probes does not correctly examine all array items.

For this project, use quadratic hashing to reimplement the hash table from Figure 12.4 on page 604.

- 5. Implement a dictionary program using a table. The user inputs a word, and the word’s definition is displayed. You will need to revise one of the table implementations to use a string as the search key. Use a hash function similar to the one you implemented for Self-Test Exercise 28.

- 6. Redo Programming Problem 12 of Chapter 10 to allow the user to search for books using the ISBN, book title, or author search key. One way to accomplish this would be to create a separate hash table of book objects for each search key; however, this would result in duplicated data and wasted memory. A better implementation would be to store the actual data in a list, and use separate hash tables for each search key. The value associated with each key is not the book itself, but just the position of the book in the book list. Assume that there are no duplicates in the search keys.

- 7. Design a scheme that allows for duplicate keys in the previous project.

- 8. Rewrite one of your hash tables so that it has additional member functions to provide statistics. You should include functions to calculate the load factor, the average number of items examined during a successful search, and the maximum number of items examined during a successful search. Find a large collection of information to put in your hash table, perhaps the list of users at your computing site. Test how the statistics vary based on the capacity of the hash table.
