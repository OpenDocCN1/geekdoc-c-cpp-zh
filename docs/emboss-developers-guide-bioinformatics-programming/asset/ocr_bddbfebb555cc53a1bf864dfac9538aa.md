# 6.18 Handling tables

# 6.18.1 Introduction

A hash table is a data structure holding key:value pairs which allows for very efficient retrieval of a value given a key. For example, a key might be the accession number of a sequence and a value might be the sequence itself. Hash tables work by translating the key into a number called a ‘hash’ using a hashing function. The hash then provides the index of an array element or ‘bucket’ in the data structure holding the value. Hash tables have the great advantage that the search time is independent of the number of items stored, and that new key:value pairs can be added efficiently.

EMBOSS supports a standard hash table using strings for keys and generic hash tables with keys of arbitrary datatype. All the basic functionality you would expect for creating, manipulating and using hash tables is provided. This includes:

+   - Hash functions for the construction of string hash functions
+   - Functions to add and remove key:value pairs or change the value associated with a key
+   - Functions to return the true key or value associated with a given key
+   - Ability to apply a function to each key:value pair
+   - Printing a string hash table.

There is no ACD datatype for hash tables, they are always created directly from within the C source code.

# 6.18.2 AJAX library files

AJAX library files for handling hash tables are listed in the table below. Library file documentation, including a complete description of datatypes and functions with usage notes is available at: http://emboss.open-bio.org/rel/dev/libs/

| Library file documentation | Description |
| --- | --- |
| ajtable | Hash table functions |

ajtable.h/c. Defines the hash table object (AjPTable) and functions for handling hash tables. They also contains static functions for handling same at a low level. You are unlikely to need the static functions unless you plan to extend the hash table code.

# 6.18.3 ACD datatypes

There are no ACD datatypes dedicated for tables.

# 6.18.4 AJAX datatypes

For handling tables use: