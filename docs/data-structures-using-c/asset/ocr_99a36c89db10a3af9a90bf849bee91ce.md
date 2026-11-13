```
{
    Hashtable[pos] = key;
    return pos;
}
else // slot is not empty
{
    for(i = pos + 1; i % MAX != pos; i++)
    {
        if(Hashtable[i] == 0)
        {
            Hashtable[i] = key;
            return i;
        }
    }
}
// Table overflow
return -1;
}
```

# Quadratic Probing

In quadratic probing, we add the offset as the square of the collision probe number. In quadratic probing, the empty location is searched by using the following formula:

(Hash(Key) + r²) MOD Max where i lies between 1 and (Max – 1)/2 (11.3)

Here if Max is a prime number of the form (4 x integer + 3), quadratic probing covers all the buckets in the table.

Quadratic probing works much better than linear probing, but to make full use of the hash table, there are constraints on the values of i and Max so that the address lies within the table boundaries. In addition, if two keys have the same initial probe position, then their sequences are the same. Similar to linear probing, the initial probe determines the entire sequence and hence maximum distinct probe sequences are used. As the offset added is not 1, quadratic probing slows down the growth of primary clusters.

Program Code 11.2 depicts this logic.

```
PROGRAM CODE 11.2
//hash function to get position
int hash(int key)
{
    return(key % MAX);
}
```