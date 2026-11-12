# FIGURE 21-5 Shifting across block boundaries

![](bbox=[0.25, 0.14, 0.75, 0.26])

add and remove for an external implementation of the ADT dictionary can require many costly file accesses due to shifting records

that, as is the case with an array-based implementation, the add and remove operations must shift dictionary items. Shifting records in an external file is, in general, far more costly than shifting array items. A file may contain an enormous number of large records, which are organized as several thousand sand blocks. As a consequence, the shifting could require a prohibitively large number of block accesses.

Consider, for example, Figure 21-5. If you insert a new record into block k, you must shift the records not only in block k, but also in every block after it. As a result, you must shift some records across block boundaries. Thus, for each of these blocks, you must read the block into internal memory, shift its records by using a statement such as

```
buf.setRecord(i+1, buf.getRecord(i))
```

and write the block to the file so that the file reflects the change. This large number of block accesses makes the external sorted array-based implementation practical only for dictionaries where insertions and removals are rare.

# 21.3.1 Indexing an External File

Two of the best external dictionary implementations are variations of the internal hashing and search-tree schemes. The biggest difference between the internal and external versions of these implementations is that in the external versions, it is often advantageous to organize an index to the data file rather than to organize the data file itself. An index to a data file is conceptually similar to other indexes with which you are familiar. For example, consider a library catalog. Rather than looking all over the library for a particular title, you can simply search the catalog. The catalog is typically organized alphabetically by title (or by author), so it is a simple matter to locate the appropriate entry. The entry for each book contains an indication (for example, a Library of Congress number) of where on the shelves you can find the book.

Using a catalog to index the books in a library has at least three benefits:

Advantages of a library catalog

+   - Because each catalog entry is much smaller than the book it represents, the entire catalog for a large library can fit into a small space. A patron can thus locate a particular book quickly.
+   - The library can organize the books on the shelves in any way, without regard to how easy it will be for a patron to scan the shelves for a particular book. To locate a particular book, the patron searches the catalog for the appropriate entry.
+   - The library can have different types of catalogs to facilitate different types of searches. For example, it can have one catalog organized by title and another organized by author.