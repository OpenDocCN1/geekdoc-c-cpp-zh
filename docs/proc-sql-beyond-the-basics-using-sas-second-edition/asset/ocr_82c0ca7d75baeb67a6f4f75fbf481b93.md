# Designing Indexes

There is no rule that says a table has to have an index, but when an index is available it can make information access and retrieval more efficient and considerably faster.

When a query is executed in SAS software, the SQL optimizer evaluates the costs associated with the available methods and uses the most efficient method to process data. Processing can occur using a sequential table scan, or with an index if one exists. When a sequential table scan is performed, SAS starts at the beginning of the table, steps row-by-row through all of the rows in the table, and processes (retrieves) rows that match the selection criteria that is specified in the WHERE clause of the query.

Indexes should be designed to provide efficient database processing when triggered (or referenced) in a query. To better understand the impact that an index has on a database application, the following things should be kept in mind:

+   - Indexes can improve the performance of queries that do not modify data because the optimizer has more choices to select from to in order to determine the fastest way to access data.

+   - A table with too many indexes might actually experience a performance degradation when using INSERT, MODIFY, or DELETE operations because all indexes must be adjusted to correspond to the changes made to the data in the table.

+   - A query that specifies an exact match comparison can benefit from an index. For example,
+   ```
+   WHERE prodnum = 5001;
+         < or >
+   WHERE prodtype = "Laptop";
+   ```

+   - A query that specifies a value between a range of values can benefit from an index. For example,
+   ```
+   WHERE invenqty BETWEEN 3 AND 10;
+         < or >
+   WHERE invenqty >= 3 AND invenqty <= 10;
+   ```

+   - Queries that produce sorted output without specifying an explicit sort operation.

+   - Queries that use a LIKE comparison operator can benefit from an index when the search pattern begins with a specific character string, such as "Lap%", but not when the search pattern begins with a wildcard, such as "%ware".

+   - Forcing the SQL optimizer to use an index in a query (with an IDXWHERE= or IDXNAME= data set option) with a small table can impede performance because SAS would traverse the

For example, once a specific part number is known, an index can be used to look up the location of the part along with its manufacturer, cost, and availability far more efficiently than with other methods. For more information about using indexes in SAS, see *The Complete Guide to Using SAS Indexes* by Michael Raithel, which is available from the SAS Bookstore.