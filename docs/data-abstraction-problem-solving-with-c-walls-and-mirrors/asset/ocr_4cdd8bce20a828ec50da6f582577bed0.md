# 664 CHAPTER 21 Processing Data in External Storage

Generally, the previous traversal is unacceptable

This traversal requires you to read a block of the data file before you display each data record; that is, the number of data-file block accesses is equal to the number of data records. In general, a large number of block accesses would not be acceptable. If you must perform this type of traversal frequently, you would probably modify the B-tree scheme so that the data file itself was kept nearly sorted.

# 21.35 Multiple Indexing

Before concluding the discussion of external implementations, let's consider the multiple indexing of a data file. Programming Problem 8 in Chapter 18 asked you to support multiple organizations for data stored in internal memory. Such a problem is also common for data stored externally. For example, suppose that a data file contains a collection of employee records on which you need to perform two types of retrievals:

```
// Retrieves the item whose search key contains the aName.
retrieved(aName: NameType): ItemType

// Retrieves the item whose search key contains the ssn.
retrieved(ssn: SSNType): ItemType
```

Multiple index files allow multiple data organizations

One solution to this problem is to maintain two independent index files to the data file. For example, you could have one index file that contains records of the form <name, pointer> and another index file that contains records of the form <socSec, pointer>. These index files could be hashed, both be B-trees, or be one of each, as Figure 21-16 indicates. The choices would depend on the operations you wanted to perform with each search key. Similarly, if an application required extremely fast retrievals on socSec and also required operations such as traverse in sorted socSec order and range queries over socSec, it might be reasonable to have two socSec index files—one hashed, the other a B-tree.

# FIGURE 21-16 Multiple index files

![](bbox=[0.268, 0.625, 0.842, 0.895])