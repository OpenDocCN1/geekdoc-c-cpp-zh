A Hash table is simply an array that is addressed via a function. For Ex. The below hash table is an array with eight elements. Each element is a pointer to a linked list of numeric data. The hash function for this example is simply divides the data key by 8, and uses the remainder as an index into the table. This yields a number from 0 to 7. Since the Range of indices for hash Table is 0 to 7. To insert a new item in the table, we hash the key to determine which list the term goes on and then insert the item at the beginning of the list. Ex to insert 11, we divide 11 by 8 whose remainder is 3. Thus, 11 goes on the list starting at hash table [3]. To find a number we hash the number and chain down the correct list to see if it is in the table. To delete a number we find the number and remove and remove the node from the linked list.

# ## 11.1 Hash Functions

The hash functions are chosen to avoid collision and also with simple operations. When we choose a particular hashing method is noted that hash function should not be biased towards any particular slot in the hash table so as to minimize collision. Also a hash function will have the characteristic that each key is likely to hash to anyone of the slots available in the hash table. Some of the hash functions are

# ### Division Method

This method is considered as a simplest method. In this method integer x is divided by M and then by using the remainder. This method is also called as the division method of hashing.