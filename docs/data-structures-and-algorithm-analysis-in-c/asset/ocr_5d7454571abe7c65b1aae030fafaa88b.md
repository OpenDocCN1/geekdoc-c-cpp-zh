randomly chosen hash functions, item A can be at either position 0 in Table 1 or position 2 in Table 2. Item F can be at either position 3 in Table 1 or position 4 in Table 2, and so on. Immediately, this implies that a search in a cuckoo hash table requires at most two table accesses, and a removal is trivial, once the item is located (lazy deletion is not needed now!).

But there is an important detail: How is the table built? For instance, in Figure 5.25, there are only three available locations in the first table for the six items, and there are only three available locations in the second table for the six items. So there are only six available locations for these six items, and thus we must find an ideal matching of slots for our six items. Clearly, if there were a seventh item, G, with locations 1 for Table 1 and 2 for Table 2, it could not be inserted into the table by any algorithm (the seven items would be competing for six table locations). One could argue that this means that the table would simply be too loaded (G would yield a 0.70 load factor), but at the same time, if the table had thousands of items, and were lightly loaded, but we had A, B, C, D, E, F, G with these hash positions, it would still be impossible to insert all seven of those items. So it is not at all obvious that this scheme can be made to work. The answer in this situation would be to pick another hash function, and this can be fine as long as it is unlikely that this situation occurs.

The cuckoo hashing algorithm itself is simple: To insert a new item, x, first make sure it is not already there. We can then use the first hash function, and if the (first) table location is empty, the item can be placed. So Figure 5.26 shows the result of inserting A into an empty hash table.

Suppose now we want to insert B, which has hash locations 0 in Table 1 and 0 in Table 2. For the remainder of the algorithm, we will use (h1, h2) to specify the two locations, so B's locations are given by (0, 0). Table 1 is already occupied in position 0. At this point there are two options: One is to look in Table 2. The problem is that position 0 in Table 2 could also be occupied. It happens that in this case it is not, but the algorithm that the standard cuckoo hash table uses does not bother to look. Instead, it preemptively places the new item B in Table 1. In order to do so, it must displace A, so A moves to Table 2, using its Table 2 hash location, which is position 2. The result is shown in Figure 5.27. It is easy to insert C, and this is shown in Figure 5.28.

Next we want to insert D, with hash locations (1, 0). But the Table 1 location (position 1) is already taken. Note also that the Table 2 location is not already taken, but we don't look there. Instead, we have D replace C, and then C goes into Table 2 at position 4, as suggested by its second hash function. The resulting tables are shown in Figure 5.29.

| Table 1 | | Table 2 | |
|---|---|---|---|
| 0 | A | 0 | |
| 1 | | 1 | |
| 2 | | 2 | |
| 3 | | 3 | |
| 4 | | 4 | |
A: 0, 2

Figure 5.26 Cuckoo hash table after insertion of A