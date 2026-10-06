# A Look at External Storage 639

FIGURE 21-2 A file partitioned into blocks of records

| B1 | B2 | B3 | B4 | ... | B5 | ... |
|---|---|---|---|---|---|---|

![](bbox=[0.315, 0.178, 0.683, 0.303])

Much as you number the elements of an array, you can now number the blocks of a file in a linear sequence. With a direct access file, a program can read a given block from the file by specifying its block number, and similarly, it can write data out to a particular block. In this regard direct access file resembles arrays of arrays, with each block analogous to a single array element, which is itself an array that contains several records.

In this direct access mode, all input and output is at the block level rather than the record level. You can read and write any block, but cannot read or write an individual record. Reading or writing a block is called a **block access**.

The algorithms in this chapter assume commands for reading and writing blocks. The pseudocode statement

```
buf.readBlock(dataFile, i)
```

will read $i^{th}$ block of datafile and place it in an object. The object must accommodate the many records that each block of datafile contains. For example, if each block contains 100 employee records, but must store at least 100 employee records. The object is called a **buffer**, which is a location that temporarily stores data as it makes its way from one process to another.

Once the system has read a block into buf, the program can process—for example, inspect or modify—the records in the buffer. Also, the records in the buffer are only copies of the records in the datafile, if a program modifies the records in buf, it must write back out to datafile, so that the file reflects the modifications. As that the statement

```
buf.writeBlock(dataFile, i)
```

will write the contents of buf to the $i^{th}$ block of the datafile. If datafile contains n blocks, the statement

```
buf.writeBlock(dataFile, n + 1)
```

will append a new block to datafile, and thus the file can grow dynamically, just as a C++ file can. Again, realize that these input and output commands allow you to read and write only entire blocks. As a consequence, even if you need to operate on a single record of the file, you must access an entire block. For example, suppose you want to give employee Smith a $1,000 raise. If Smith's record is in block $i$ (how to determine the correct block is discussed later in the chapter), you would perform the following steps:

```
// read block i from dataFile into buffer buf
buf.readBlock(dataFile, i)
```