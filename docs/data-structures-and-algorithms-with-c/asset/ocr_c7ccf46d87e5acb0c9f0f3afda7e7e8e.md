+   - The relation is only a few pages long. In this case, the time to locate any tuple is Short, even if the entire relation has been searched serially.
+   - When every tuple in the relation has to be retrieved (in any order) every time the relation is accessed. For example, retrieve the name of all the students.

# Disadvantages

+   - Heap file organization is not good when we deal with selected records of a file, this will increase processing time and thus degrade the performance.

# Hash File organization

In hash file organization the records are stored in the file using a hash function. A hash function is defined over a key field and that field is known as Hash Field. Hash function generates a value which is mapped to the key and accordingly the record is placed in the file. This file organization is also termed as Direct or Random file organization. These types of files are used in a direct access storage device (DASD) like a floppy disk, computer disk, optical disk, etc. in such storage devices, the records are stored in random order that allows immediate access as direct access to the individual records. Commonly some arithmetic function is applied to the hash field so that the records will be evenly distributed throughout the file.

# Advantages

+   - Access and retrieval of records become easy and fast.
+   - Transaction need not be sorted and placed in sequence prior to processing.
+   - Accumulation of transactions into batches is not required before processing them.
+   - Immediate updating of several files as a result of the single transaction is possible.

# Disadvantages

+   - These files must be stored on a direct- access storage device. Hence, relatively expensive hardware and software resources are required.
+   - Special precaution should be taken during manipulation of records.
+   - Updating of records becomes difficult.
+   - Less efficient than sequential file organization.

# Index Sequential File Organization

In this file organization the records are organized in a sequential manner. The difference with Sequential file organization is that here an index table is maintained for easy and fast access to the record. The records of the files can be stored in a random sequence but the index table is in a sorted sequence on the key value. The file management system simply accesses the data records in the order of the index value. These, indexed sequential files provide the user sequential access, even though the file management system is accessing the data records in a physically random order.

+   Index file contains two fields
+   i) Index field
+   ii) Pointer field

Depending upon these two fields, file indexing is categorized into following classes:

# Primary Index

If the primary key of the table is used as an index field then the corresponding indexing is known as