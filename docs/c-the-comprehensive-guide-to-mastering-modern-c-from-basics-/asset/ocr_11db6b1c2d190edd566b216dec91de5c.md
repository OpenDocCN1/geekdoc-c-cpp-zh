loops.

# Specialty: By the Bucketful

You can gain insights into the hash table with bucket_count, bucket_size, and bucket. With begin(int) and end(int), you get iterators to the elements of a specific bucket.

# Specialty: Reserve Space

With reserve Or rehash, you can influence how large the hash table should become so that the table is not immediately rearranged during upcoming insert operations and iterators remain valid. load_factor and max_load_factor are the interfaces to the table's load factor.