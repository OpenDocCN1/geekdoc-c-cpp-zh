# 9.4 Hashing

335

```
// Search for the record with Key K
template <typename Key, typename Value>
hashdict<Key, Value>::
hashSearch(const Key& k) const {
    int home;
    int pos = h(k); // Initial position is home slot
    for (int i = 0; k != (HT[pos].key()) && EMPTY; i++)
        pos = (home + p(k, i)) % M; // Next on probe sequence
    if (k == (HT[pos].key()) // Found it
        return (HT[pos].value());
    else return NULL; // not in hash table
```

Figure 9.7 Search method for a dictionary implemented by a hash table.

That, the $i$th of the probe sequence is just $i$, meaning that the $i$th step is simply to move $i$ slots in the table.

Once the bottom of the table is reached, the probe sequence wraps around to the beginning of the table. Linear probing has the virtue that all slots in the table will be candidates for inserting a new record before the probe sequence returns to the home position.

While linear probing is probably the first idea that comes to mind considering collision resolution policies, it is not the only one possible. In fact, linear probing is one of the worst collision resolution methods. The main problem is illustrated by Figure 9.8. Here, we use a hash table of slots to store four-digit numbers, with hash function $h(k) = k \mod 10$. In Figure 9.8(a), five numbers have been placed in the table, leaving five slots remaining.

The ideal behavior for a collision resolution mechanism is that each slot in the table will have equal probability of receiving the next inserted record (assuming that every slot in the table has equal probability of being hashed to initially). In this example, the hash function gives each slot (roughly) equal probability of being the home position for the next key. However, consider what happens when the next key has its home position at slot 0. Linear probing will send the record to slot 2. The same will happen to records whose home position is slot 1. A record with home position at slot 2 will remain in slot 2. Thus, the probability is 3/10 that the record inserted will end up in slot 2. In a similar manner, records hashing to slot 7 or 8 will end up in slot 9. Only records hashing to slot 3 will be stored in slot 3, yielding one chance in happening. Likewise, one chance in ten that the next record will be stored in slot 4, one chance in ten for slot 5, and one chance in ten for slot 6. Thus, the resulting probabilities are not equal.

To make matters worse, if the record ends up in slot 9 (which already has a higher than normal chance of happening), then the following record will end up