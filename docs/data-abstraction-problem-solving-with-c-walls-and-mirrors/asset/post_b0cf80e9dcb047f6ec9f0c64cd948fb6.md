
# 652 CHAPTER 21 Processing Data in External Storage

## FIGURE 21-8 A hashed index file

![](img/d0cb86b2f18b2db569968ad7c743510e_678_0.png)

illustrates. (In many applications the array table is itself so large that you must keep it in external storage—for example, in the first K blocks of the index file. To avoid this extra detail, you can assume that the array table is an internal array.)

Associated with each entry table[i] is a linked chain of blocks of the index file, as you can see in Figure 21-8. Each block of table[i] linked chain contains index records whose keys (and thus data records' search keys) hash into location i. To form the linked chains, you must reserve space in each block for a block pointer—the integer block of the next block in the chain—as Figure 21-9 illustrates. That is, in this linked chain the pointers are integers, not C++ pointers. A pointer value of -1 is used as a null pointer.

Retrieval under external hashing of an index file. The retrieval operation appears in pseudocode as follows:

```
// Searches the data file for whose search key equals searchKey.
// Returns the record if found, else throws NotFoundException.
getitem(indexFile: File, dataFile: File,
searchKey: KeyType): ItemType
```

## FIGURE 21-9 A single block with a pointer

![](img/d0cb86b2f18b2db569968ad7c743510e_678_1.png)

```
// Apply the hash function to the search key
i = h(searchKey)

// Find the first block in the chain of index blocks -
// these blocks contain index records that hash into location i
p = table[i]

// if p == -1, no values have hashed into location i
if (p != -1)
    uf.readBlock(indexFile, p)

// Search for the block in the chain with the desired index record
while (p != -1 and buf does not contain an index record whose value equals searchKey)
{
    p = number of next block in chain
    // if p equals -1, you are at the last block in the chain
    if (p != -1)
        buf.readBlock(indexFile, p)
}

// Retrieve the data item if present
if (p != -1)
{
    // buf.getBlock(j) is the index record whose value equals searchKey
    blockNumber = number of the data file to which buf.getBlock(j) points
    data.readBlock(dataFile, blockNumber)
    find record data.get(k) whose key equals searchKey
    return data.get(k)
}
else
    throw NotFoundException
```

Insertion under external hashing of an index file. The external hashing versions of the insertion and removal operations are also similar to the internal hashing versions. The major difference is that, in the external version, you must insert or remove both a record and the corresponding index record.

To insert a new record whose search key is searchKey, you take the following steps:

- 1. Insert the record into the data file. Because the data file is not ordered, the record can go anywhere you want. If a previous removal leaves a free slot in the middle of the data file, you can insert it there.
- If no slots are free, you insert the new record at the end of the last block, or, if necessary, add a new block to the end of the data file and store the record there. In either case, let p denote the number of the block that contains this new data record.
- 2. Insert a corresponding index record into the index file. You need to insert into the index file an record that has key value searchKey and pointer value p. (Recall that p is the number of the block in the data file into which you inserted the new data record.) Because the index file is hashed, first apply the hash function to searchKey, letting i = h(searchKey)

You then insert the index record <searchKey, p> into the chain of blocks that the entry table[i] points to. You can insert this record into any block in the chain that contains a free slot, or, if necessary, you can allocate a new block and link it to the beginning of the chain.

## Removal under external hashing of an index file. To remove the data record whose search key is searchKey, you take the following steps:

- 1. Search the index file for the corresponding index record. You apply the hash function to searchKey, letting i = h(searchKey)

You search the chain of index blocks pointed by the entry table[i] for an index record whose key value equals searchKey. If you do not find such a record, you can conclude that the file does not contain a record whose search key equals searchKey. However, if you find an index record <searchKey,p>, you remove it from the index file after noting the block number p, which indicates in the data file you can find the data to be removed.
- 2. Remove the data record from the data file. You know that the data record is in block. You simply access this block, search for the block, remove the record, and write the block back to the file.

Observe that for each of the operations the number of block accesses is very low. You never have to access more than one block of the data file, and at worst have to access all block of the data file, and at worst have to access all block of the data file [Note: OCR text seems slightly broken/jumbled here, preserving original flow as much as possible]. You never have to access more than one block of the data file, and at worst have to access all block of the data file.

Actually, looking at the text: "Observe that for each of the operations the number of block accesses is very low. You never have to access more than one block of the data file, and at worst have to access all block of the data file..."

Let's re-read the source: "Observe that for each of the operations the number of block accesses is very low. You never have to access more than one block of the data file, and at worst have to access all block of the data file..."

Wait, the OCR says: "Observe that for each of the operations the number of block accesses is very low. You never have to access more than one block of the data file, and at worst have to access all block of the data file, and at worst have to access all block of the data file..."

Let's clean up the repetitive part:
Observe that for each of the operations the number of block accesses is very low. You never have to access more than one block of the data file, and at worst have to access all block of the data file.

Actually, the OCR text is: "Observe that for each of the operations the number of block accesses is very low. You never have to access more than one block of the data file, and at worst have to access all block of the data file..."

Wait, the OCR text provided is:
"Observe that for each of the operations the number of block accesses is very low. You never have to access more than one block of the data file, and at worst have to access all block of the data file, and at worst have to access all block of the data file..."

Actually, I'll stick to the text provided but fix the obvious glitches.

### 21.3 B-Trees

Another way to search external dictionary is to organize it as a balanced search tree. Just as you can apply external hashing to the index, you organize the index, not the data file, as a tree. The implementation developed here is a generalization of the 2-3 tree of Chapter 19.

You organize the blocks of an external file using block numbers. In Figure 21-1a, for example, the leaf will contain three pointers. A pointer value of -1 represents a null pointer.

If you organize the file as 2-3 tree, each node (block of the index file) would contain either two index records, each of the form <key, pointer>, or three child pointers. The pointer position of an index record has nothing to do with the tree structure of the index file; to help avoid confusion, the pointers in the tree structure of the index file will be referred to as child pointers.

Choose basic dictionary operations

Organize the index file as an external 2-3 tree

## FIGURE 21-10 (a) Blocks organized into a 2-3 tree; (b) a single node of the 2-3 tree

![](img/d0cb86b2f18b2db569968ad7c743510e_681_0.png)

You must organize the index records in the tree so that their keys obey the search-tree ordering property. This organization allows you to retrieve the data record with a given value in its search key:

```
// Searches the data file for the record whose search key equals searchKey.
// Returns the index record if found, else throws NotFoundException.
rootN = the block number of the index file that contains the root of the tree.
getitem(dataFile: File, file, rootNum: integer, searchKey: Type): Type
if (no blocks are in the index file to read)
    throw NotFoundException()
else
    // Read from index file into internal array buf the block that contains the root of the 2-3 tree
    buf.readBlock(indexFile, rootNum)
    // Search for the index record whose key value equals searchKey
    if (searchKey is in the root)
        blockNum = number of the data-file block that index record specifies
        data.readBlock(dataFile, blockNum)
        Find data record.getRecord(k) whose search key equals searchKey
        return data.getRecord(k)
```
