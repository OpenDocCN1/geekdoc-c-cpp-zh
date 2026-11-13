We have studied the representation of and operations on various data structures such as arrays, stacks, queues, linked lists, trees, and graphs. The storage representations and data manipulations described are applied only to data entities, which reside in the main memory. In many situations, all information that is to be processed does not reside in the main memory. There are two reasons for this. First, there are some large programs and data, which cannot fit conveniently into the main memory. Secondly, it is often desirable or necessary to store information from one run of a program to the next run. Let us consider a student's information system. We need the data to be preserved even after the execution of the program is over. Therefore, large volumes of data and archival data are commonly stored in external memory as special data holding entities—files.

Each record contains attributes to describe one entity. Generally, all records for one entity type are usually of the same form. Mostly, each of them has the same fields in the same quantity, order, and length. Such records are known as fixed length records. Structures in C/C++ support this type of record.

Records that are not necessarily of the same length are known as variable length records. C/C++ unions support this type of record. Variable length records are less common than fixed length records, as they are more difficult to handle. They tend to complicate the storage schemes and are sometimes impractical for some structures. When variable records are used, we need to maintain more information about each record.

Magnetic tapes, floppy disks, and hard disks are a few examples of secondary storage devices. When data is organized in a file data structure, the data is non-volatile, which means that the data will reside on storage after data processing is over.

# 14.2 EXTERNAL STORAGE DEVICES

For persistent storage, large volumes of data and archival data are commonly stored in external memory as special data holding entities, namely files. Before we learn about file organization and operations on files, let us discuss the storage devices, which hold the files.

The external storage devices are those on which information or data can be stored and from which it can be retrieved. The data resides on these devices as a non-volatile memory. The storage and retrieval operations are known as writing and reading, respectively. Capacity of external storage devices is larger than that of the main memory and is also slower and less expensive per bit of information stored when compared to the main memory.

External storage devices are mainly used for the following:

+   1. Overlay or backup of programs during execution
+   2. Storage of programs for future use
+   3. Storage of information in files

We shall mainly concentrate on the third use, discuss the most common external storage devices in the order of their uses, and study magnetic tapes, drums, and disk drives.