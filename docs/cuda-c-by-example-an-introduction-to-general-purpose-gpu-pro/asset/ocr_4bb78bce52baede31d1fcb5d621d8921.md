As described in the introductory section, the structure Entry holds both a key and a value. In our application, we will use unsigned integer keys to store our key/value pairs. The value associated with this key can be any data, so we have declared value as a void * to indicate this. Our application will primarily be concerned with creating the hash table data structure, so we won't actually store anything in the value field. We have included it in the structure for completeness, in case you want to use this code in your own applications. The last piece of data in our hash table Entry is a pointer to the next Entry. After collisions, we'll have multiple entries in the same bucket, and we have decided to store these entries as a list. So, each entry will point to the next entry in the bucket, thereby forming a list of entries that have hashed to the same location in the table. The last entry will have a NULL next pointer.

At its heart, the Table structure itself is an array of “buckets.” This bucket array is just an array of length count, where each bucket in entries is just a pointer to an Entry. To avoid incurring the complication and performance hit of allocating memory every time we want to add an Entry to the table, the table will maintain a large array of available entries in pool. The field firstFree points to the next available Entry for use, so when we need to add an entry to the table, we can simply use the Entry pointed to by firstFree and increment that pointer. Note that this will also simplify our cleanup code because we can free all of these entries with a single call to free (). If we had allocated every entry as we went, we would have to walk through the table and free every entry one by one.

After understanding the data structures involved, let’s take a look at some of the other support code:

```
void initialize_table( Table *table, int entries,
                       int elements ) {
  table.count = entries;
  table.entries = (Entry**)calloc( entries, sizeof(Entry*) );
  table.pool = (Entry*)malloc( elements * sizeof( Entry ) );
  table.firstFree = table.pool;
}
```