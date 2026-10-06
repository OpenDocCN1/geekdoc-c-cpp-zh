# 646 CHAPTER 21 Processing Data in External Storage

```
while (in1 is not exhausted)
// Invariant: out is ordered
Place item of in1 into the next position of out

while (in2 is not exhausted)
// Invariant: out is ordered
Place item of in2 into the next position of out

out.writeBlock(toFile, next block of toFile)
// Finish off the remaining complete blocks

while (blocks remain in Run 1)
  // Invariant: Each block in toFile is ordered
  in1.readBlock(fromFile, next block of Run 1)
  in1.writeBlock(toFile, next block of toFile)


while (blocks remain in Run 2)
  // Invariant: Each block in toFile is ordered
  in2.readBlock(fromFile, next block of Run 2)
  in2.writeBlock(toFile, next block of toFile)
```

# 21.3 External Dictionaries

![](bbox=[0.137, 0.473, 0.196, 0.493])

This section discusses techniques for organizing records in external storage so that you can efficiently perform ADT dictionary operations such as retrieval, insertion, removal, and traversal. Although this discussion will only scratch the surface of the topic, you have a head: Two of the most important external dictionary implementations are variations of hashing and the 2-3 tree, which you studied in Chapters 18 and 19.

A simple external dictionary implementation: records stored in search-key order

Suppose that you have a direct access file of records that are to dictionary items. The file is partitioned into blocks, as described earlier in this chapter. One of the simplest dictionary implementations stores the records by their search key, perhaps sorting the file by using an external merge sort algorithm developed in the previous section. Once it is sorted, you can easily traverse the file in sorted order using the following algorithm:

Sorted-order traversal

```
// Travers the sorted file dataFile in sorted order;
// calling function visit once for each item
traverse(dataFile: file, numberOfBlocks: integer,
        recordsPerBlock: integer, visit: FunctionType)
// Read each block of dataFile into an input buffer
for (blockNumber = 1; blockNumber <= numberOfBlocks)
  buf.readBlock(dataFile, blockNumber)
  // Visit each record in the block
  for (recordNumber = 1; recordNumber <= recordsPerBlock)
    visit buf.getRecord(recordNumber-1)
```

To perform the retrieval on the sorted file, you can use a binary search algorithm as follows:

```
// Searches blocks through last of the file dataFile
// for the record whose search key equals searchkey
```