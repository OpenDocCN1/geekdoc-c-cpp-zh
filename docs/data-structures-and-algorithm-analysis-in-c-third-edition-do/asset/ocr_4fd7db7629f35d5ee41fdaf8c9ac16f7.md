| 1 | 2003 | 5894 | 10528 |
|---|---|---|--|
| Second Level Index | | | | |
| 1 | 2001 | 2003 | 5688 | 5894 | 9942 | 10528 | 10984 |
| Linear Index: Disk Blocks | | | | | |

**Figure 10.2** A two-level linear index. The linear index is stored on disk. The smaller, second-level index is stored in main memory. Each element in the second-level index stores the first value in the corresponding disk block of the index file. Thus, the first disk block of the linear index stores keys in the range 1 to 2003 to 5688. Thus, the first entry of the second-level index is key value 1 (the first key in the first block of the linear index), while the second entry of the second-level index is key value 2003.

second-level index is stored in main memory, accessing a record by this method requires two reads: one from the index file and one from the database file for the actual record.

Every time a record is inserted or deleted from the database, all associated secondary indices must be updated. Updates to a linear index are expensive, because the contents of the array may be shifted. Another problem is that multiple records with the same secondary key may duplicate that key value within the index. When the secondary key field has many duplicates, such as when it has a limited range (e.g., a field to identify job category from a small number of possible job categories), this duplication might waste considerable space.

One improvement on the sorted array is a two-dimensional array where each row corresponds to a secondary key value. A row contains the primary keys whose records have the indicated secondary value. Figure 10.3 illustrates this approach. Now there is no duplication of key values, possibly yielding a considerable space savings. The cost of insertion and deletion is reduced, because only one row of the table needs be adjusted. Note that a new row is added to the array when a new secondary key is added, but this will happen frequently in applications suited to using this arrangement.

A drawback to this approach is that the array must be of fixed size, which imposes an upper limit on the number of primary keys that might be associated with a particular secondary key. Furthermore, those secondary keys with fewer records than the width of the array will waste the remainder of the row. A better approach is to have a one-dimensional array of secondary key values, where each secondary key is associated with a linked list. This works well if the index is stored in main memory, but not well when it is stored on disk because the linked list for a given key might be scattered across several disk blocks.