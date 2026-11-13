as: 1000 + (5-1) * 20 = 1000 + 80 = 1080

Table 16.3 summarizes the features, advantages, and disadvantages of relative file organization.

# Table 16.3 Relative file organization

| Features | Advantages | Disadvantages |
| :--- | :--- | :--- |
| • Provides an effective way to access individual records | • Ease of processing | • Use of relative files is restricted to disk devices |
| • Records number represents the location of records relative to the beginning of the file | • If the relative record number of the record that has to be accessed is known, then the record can be accessed directly | • Fixed amount of storage space can be allocated |
| • Records in a relative file are of fixed length | • Random access of records makes access to relative files fast | • For random access of records, the relative record number must be known in advance |
| • Relative files can be used for both random as well as sequential access | • Allows deletions and updations in the same file | |
| • Every location in the table either stores a record or is marked as FREE | • Provides random as well as sequential access of records with low overhead | |
| | • New records can be easily added in the free locations based on the relative record number of the record to be inserted | |
| | • Well suited for interactive applications | |

# 16.6.3 Indexed Sequential File Organization

Indexed sequential file organization stores data for fast retrieval. The records in an indexed sequential file are of fixed length and every record is uniquely identified by a key field. We maintain a table known as the *index table* which stores the record number and the address of all the records. That is for every file, we have an index table. This type of file organization is called indexed sequential file organization because physically the records may be stored anywhere, but the index table stores the address of those records.

The ith entry in the index table points to the ith record of the file. Initially, when the file is created, each entry in the index table contains NULL. When the ith record of the file is written, free space is obtained from the free space manager and its address is stored in the ith location of the index table.

| Record number | Address of the Record |
| :--- | :--- |
| 1 | 765 |
| 2 | 27 |
| 3 | 876 |
| 4 | 742 |
| 5 | NULL |
| 6 | NULL |
| 7 | NULL |
| 8 | NULL |
| 9 | NULL |

Figure 16.5 Indexed sequential file organization

Now, if one has to read the 4th record, then there is no need to access the first three records. Address of the 4th record can be obtained from the index table and the record can be straightway read from the specified address (742, in our example). Conceptually, the index sequential file organization can be visualized as shown in Fig. 16.5.

An indexed sequential file uses the concept of both sequential as well as relative files. While the index table is read sequentially to find the address of the desired record, a direct access is made to the address of the specified record in order to access it randomly.

Indexed sequential files perform well in situations where sequential access as well as random access is made to