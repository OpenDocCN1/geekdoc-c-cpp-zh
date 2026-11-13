+   - Inverted files are frequently used indexing technique in document retrieval systems for large textual databases. An inverted file reorganizes the structure of an existing data file in order to provide fast access to all records having one field falling within set limits.
+   - Majority of the database management systems use B-tree indexing technique. The index consists of a

+   - hierarchical structure with upper blocks containing indices pointing to the lower blocks and lowest level blocks containing pointers to the data records.
+   - Hashed file organization uses hashed indices. Hashing is used to calculate the address of disk block where the desired record is stored. If x is the set of all search key values and B is the set of bucket addresses, then a hash function H maps K to B .

# EXERCISES

+   ## Review Questions
+   1. Why do we need files?
+   2. Explain the terms field, record, file organization, key, and index.
+   3. Define file. Explain all the file attributes.
+   4. How is archive attribute useful?
+   5. Differentiate between a binary file and a text file.
+   6. Explain the basic file operations.
+   7. What do you understand by the term file organization? Briefly summarize the different file organizations that are widely used today.
+   8. Write a brief note on indexing.
+   9. Differentiate between sparse index and dense index.
+   10. Explain the significance of multi-level indexing with an appropriate example.
+   11. What are inverted files? Why are they needed?
+   12. Give the merits and demerits of a B-tree index.

+   ## Multiple-choice Questions
+   1. Which of the following flags is cleared when a file is backed up?
+   (a) Read-only
+   (b) System
+   (c) Hidden
+   (d) Archive
+   2. Which is an important file used by the system and should not be altered or removed from the disk?
+   (a) Hidden file
+   (b) Archived file
+   (c) System file
+   (d) Read-only file
+   3. The data hierarchy can be given as

+   (a) Fields, records, files and database
+   (b) Records, files, fields and database
+   (c) Database, files, records and fields
+   (d) Fields, records, database, and files

+   4. Which of the following indexing techniques is used in document retrieval systems for large databases?
+   (a) Inverted index
+   (b) Multi-level indices
+   (c) Hashed indices
+   (d) B-tree index

+   ## True or False
+   1. When a backup program archives the file, it sets the archive bit to one.
+   2. In a text file, data is stored using ASCII codes.
+   3. A binary file is more efficient than a text file.
+   4. Maintenance of a file involves re-structuring or re-organization of the file.
+   5. Relative files can be used for both random access of data as well as sequential access.
+   6. In a sparse index, index table stores the address of every record in the file.
+   7. Higher level indexing must always be sparse.
+   8. B-tree indices are most suitable for highly selective columns.

+   ## Fill in the Blanks
+   1. ______ is a block of useful information.
+   2. A data field is usually characterized by its ______ and ______.
+   3. ______ is a collection of related data fields.