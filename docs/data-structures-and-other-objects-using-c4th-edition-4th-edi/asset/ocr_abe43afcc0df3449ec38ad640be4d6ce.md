+   10. Programmers tend to use a struct only when all the members are public.

+   11. Collisions are resolved by placing the item in the next open spot of the array.

+   12. Here's the body of the implementation:
+   
+   ```
+   {
+   bool found;
+   std::size_t index;
+   assert(key >= 0);
+   find_index(key, found, index);
+   return found;
+   }
+   ```

+   13. Here's the body of the implementation:
+   
+   ```
+   {
+   std::size_t index;
+   assert(key >= 0);
+   find_index(key, found, index);
+   if (found)
+       result = data[index];
+   }
+   ```

+   14. Here is the never_used member function:
+   
+   ```
+   template <class RecordType>
+   inline bool Table<RecordType>::
+   never_used(size_t index) const
+   // Library facilities used: stdlib.h
+   // Precondition: index < CAPACITY.
+   // Postcondition: if data[index] has never
+   // been used, then the return value is true.
+   // Otherwise the return value is false.
+   {
+       return
+       (data[index].key == NEVER_USED);
+   }
+   ```
+   
+   Here is the is_vacant member function:
+   
+   ```
+   template <class RecordType>
+   inline bool Table<RecordType>::
+   is_vacant(size_t index) const
+   // Library facilities used: stdlib.h
+   // Precondition: index < CAPACITY.
+   // Postcondition: If data[index] is not now
+   // being used, then the return value is true.
+   // Otherwise the return value is false.
+   {
+       return
+       (data[index].key < 0);
+   }
+   ```

+   15. If the key was already present, then the record with that key is overwritten. If the key was not already present, then the assertion tests whether size() < CAPACITY is true, and this assertion fails, halting the program.

+   16. Suppose we start looking in the data array at some index, say 34, and we move forward until we find an unoccupied location. Perhaps this first unoccupied location is at index 36. If position 36 has a key of NEVER_USED, then that indicates that the position has never been used, and therefore no record with the given key appears in the array (since it would have been placed in this unused position, or perhaps in position 34 or 35, which we already examined).
+   
+   On the other hand, if position 36 has a key of PREVIOUSLY_USED, then this position has previously been used and since removed. In this case, it is possible that there is a record with the given key in the array at a position after data[36]. It might be at this position, because at the time it was inserted, data[36] might have been in use.

+   17. Linear probing can result in clustering of elements when several different keys are hashed to the same location. Insertions and searching take longer as clustering gets worse. Double hashing can solve this problem by using a second hash function to resolve a collision.

+   18. For linear probing, the key/index pairs are 103 at [0], 0 at [1], 205 at [102], 308 at [2], 411 at [3], and 2 at [4]. For double hashing the key/index pairs are 103 at [0], 0 at [1], 205 at [102], 308 at [5], 411 at [7], and 2 at [2].

+   19. There is a twin prime pair at 1229 and 1231, which suggests that 1231 is a good table capacity.

+   20. NULL

+   21. We suggest that you first write a helper function with one parameter that is a key. The function returns a pointer to a node with the specified key (or returns NULL if there is no