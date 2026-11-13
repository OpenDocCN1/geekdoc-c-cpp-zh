such node). Using this function (which we call find_ptr), the implementation is:

```
```cpp
template <class RecordType>
void Table<RecordType>::
insert(const RecordType& entry)
{
    main_savv_6B::node<RecordType>
    *cursor;

    cursor = find_ptr(entry.key);
    if (cursor == NULL)
    {
        list_head_insert
        (data[hash(entry.key)], entry);
        ++used;
    }
    else
        cursor->setdata(entry);
}
```
```

22. The data[0] list will have the keys 0 and 811. The data[1] list will have the keys 1623. The data[2] list will have the keys 2 and 2435. The data[3] list will have the key 3247. All other lists are empty.

23. The ADT does use dynamic memory (the linked lists).

24. If the lists are kept in order, then a search can stop as soon as it reaches a key that is greater than the target.

25. The load factor is 0.9 (i.e. 180/200). With linear probing, the expected average is 5.50; with double hashing, the expected average is 2.56; with chained hashing, the expected average is 1.45.

26. For linear probing, we need a load factor of 2/3, which requires a table capacity of 1500. For double hashing, we need a load factor of just less than 0.8, requiring a table capacity of about 1250. For chaining, we need a load factor of 2, requiring an array size of 500.

27. A template parameter can be a data type, a constant data value, or a function.

28. Here is one implementation:

```
```cpp
int hashkey(const string& s)
{
    int result = 0;

    for (int i = 0; i < s.length(); ++i)
        result = result + static_cast<int>(s[i]);

    return (result % table_size);
}
```
```

29. Here is one implementation:

```
```cpp
bool table::is_present(int key) const;
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
```

30. A copy constructor, destructor, and assignment operator are needed only when a class makes direct use of dynamic memory. The new table class uses dynamic memory, but only through the vector class, which is another great reason to use the STL classes.