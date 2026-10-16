An assortment of novel approaches has been used to rename tables. One approach, which is shown below, uses the CREATE TABLE statement with the SELECT query to create a new table with the desired table name, followed by the DROP TABLE statement to delete the old table. You should be aware, however, that this is not an efficient method to rename a table.

# SQL Code

```
PROC SQL;
    CREATE TABLE MANUFACTURED_PRODUCTS AS
        SELECT *
            FROM PRODUCTS;
    DROP TABLE PRODUCTS;
QUIT;
```

# Indexes

In database systems, an index is a data structure that is used to locate specific rows of data in a table. A keyword or other identifier is used by the index to search for specific rows of interest. To better understand what an index is, it is useful to imagine an index that is located at the end of a book. In its purest form, the book’s index contains keywords that are listed in alphabetical order along with the corresponding page numbers displayed in ascending order, as shown in Figure 6.1. An index is typically made available to enable readers to skip around to different pages or locations in a book. It is worth mentioning that for an index to retain its intrinsic value, the keyword and page number must correctly access the desired page(s) of interest. A more traditional approach to reading a book is in a page-by-page sequential manner. These different approaches are often referred to as direct access versus sequential access, respectively.

Figure 6.1: Keyword Index in Book

![](bbox=[0.18, 0.6, 0.55, 0.82])