# (FIGURE 12.6 continued)

```
template <class RecordType>
inline std::size_t table<RecordType>::hash(int key) const
// Postcondition: The return value is the hash value for the given key.
{
    return (key % CAPACITY);
}
```

```
template <class RecordType>
inline std::size_t table<RecordType>::next_index(std::size_t index) const
// Precondition: index < CAPACITY.
// Postcondition: The return value is either index+1 (if this is less than CAPACITY) or zero
// (if index+1 equals CAPACITY).
{
    return ((index+1) % CAPACITY);
}
```

```
template <class RecordType>
void table<RecordType>::find_index(const int key, bool& found, std::size_t& i) const
// Precondition: key >= 0.
// Postcondition: If a record is in the table with the specified key, then found is true and index
// is set so that data[index].key is the specified key. Otherwise found is false, and i is garbage.
{
    std::size_t count; // Number of entries that have been examined

    count = 0;
    i = hash(key);
    while((count < CAPACITY) && (!never_used(i)) && (data[i].key != key))
    {
        ++count;
        i = next_index(i);
    }
    found = (data[i].key == key);
}
```

```
template <class RecordType>
inline bool table<RecordType>::never_used(std::size_t index) const
| See the solution to Self-Test Exercise 14 on page 626.
```

```
template <class RecordType>
inline bool table<RecordType>::is_vacant(std::size_t index) const
| See the solution to Self-Test Exercise 14 on page 626.
}
```