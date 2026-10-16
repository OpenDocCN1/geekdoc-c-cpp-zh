
> Note: When you create a join without a WHERE clause, you are creating an internal, virtual table called a Cartesian product. This table can be extremely large because it represents all possible combinations of rows and columns in the joined tables.

## DATA Step Merges versus PROC SQL Joins

The purpose of this section is to briefly explain the differences (and similarities) between DATA step merges and PROC SQL joins. The reason for addressing this topic is that over the years questions have been asked about which approach is superior, inferior, faster, slower, better, worse, easier, harder, more efficient, less efficient, more demanding on a programmer’s time, less demanding on a programmer’s time, more supportable, less supportable, etc. My usual reply mentions that, “Only you and your organization will be able to answer this question completely, and here’s why.”

Besides the obvious syntax and implementation method differences with the merge using a DATA step construct and the join using a procedure supplied by SAS, both approaches achieve essentially the same results. In fact, both approaches combine two or more data sets (or tables) horizontally by matching keys, and are able to process one-to-one, one-to-many, many-to-one, and many-to-many matched combinations. Table 7.1 provides a few considerations that every SAS and SQL user should ask and answer before deciding which approach is most appropriate to use.

## Table 7.1: Merge versus Join Features/Considerations

| Features / Considerations | DATA Step Merge | PROC SQL Join |
|---|---|---|
| Is there a limit to the number of data sets (or tables) that can be processed, other than disk space? | No | Yes (Limit of 256 tables) |
| Is the code portable to other database implementations? | No | Yes |
| Is the approach a standardized method for specifying database requests? | No | Yes |
| Does a sort need to be performed for processing BY-groups? | Yes | No |
| Is a common variable name required when combining data sets (or tables)? | Yes | No |
| When combining data sets (or tables) is the duplicate matching column automatically overlaid? | Yes | No |
| Are the results automatically printed after combining data sets (or tables)? | No | Yes |

## Types of Complex Queries

The SQL procedure supports a number of complex query constructs (sometimes referred to as join types). From inner joins to left, right, and full outer joins, this chapter provides a comprehensive look at the various forms of SELECT statements that can be constructed to manipulate and transform multiple tables. The SQL procedure supports four categories of data relationships: one-to-one, one-to-many, many-to-one, and many-to-many, where each category is classified by how the rows in each table relate to one another.

One-to-one relationships represent the simplest of join operations. It’s characterized by the tables that have a BY-group column with no repeats of BY-values (a unique BY-column) in any of the tables. It assumes that the rows of data in each table are in the exact same relative order, where the combined results will comprise row one in table one with row one in table two, row two in table one with row two in table two, row three in table one with row three in table two, and so on

One-to-many and many-to-one relationships are no more complicated than one-to-one relationships, and are easily represented by the SQL procedure. These types of relationships are characterized by one table having no repeats of BY-values and the other table having one or more repeats of BY-values.

Many-to-many relationships can be a bit more complicated than one-to-one, one-to-many, and many-to-one relationships. Many-to-many relationships are characterized by all tables having one or more repeats of by-values. There are notable advantages of using the SQL procedure to perform these types of joins. First, the column names from the source tables do not have to be identically named. Second, pre-sorting the tables is not necessary because the SQL optimizer will determine whether any indexes are available (see Chapter 6, “Modifying and Updating Tables and Indexes”) or if ordering the data is necessary using an implied ORDER BY clause.

Additional topics and examples include subqueries and set operations such as UNION, INTERSECT, and EXCEPT operators. Table 7.2 presents the various types of complex queries that are available in the SQL procedure.

## Table 7.2: Types of Complex Queries

| Query Type | Description |
|---|---|
| Cartesian Product or Cross Join | A join that creates a table that represents all of the combinations of rows and columns from two or more tables. It is represented by the absence of a WHERE clause. |
| Inner Joins | A join that only retrieves rows with matching values from two or more tables (maximum of 256 tables). This type of join is referred to as a conventional type of join. |
| Equijoin | A join with an equality condition (for example, equal sign “=”) specified between columns in two or more tables. |
| Non-Equijoin | A join with an inequality condition (for example, NE, >, <) specified between columns in two or more tables. |
| Reflexive or Self Join | A join that combines a table with itself. |
| Outer Joins | A join that retrieves rows with matching values while preserving some or all of the unmatched rows from one or both tables (maximum of 2 tables). |
| Left Outer Join | A join that preserves unmatched rows from the left table. |
| Right Outer Join | A join that preserves unmatched rows from the right table. |
| Full Outer Join | A join that preserves unmatched rows from the left and right tables. |
| Subqueries | A query within another query, which is sometimes referred to as a nested query, that retrieves rows from one table based on values in another table. |
| Simple Subquery | A self-contained and independent query within another query that returns single or multiple values from an inner query. |
| Correlated Subquery | An outer query that passes value(s) to an inner query that after execution passes the results back to the outer query. |
| Set Operations | These operators combine or concatenate query results vertically. |
| UNION | Combines all unique (non-duplicate) rows from both queries. |
| INTERSECT | Combines all matched rows from the first query with rows in the second query. |
| EXCEPT | Produces rows from the first query that do not appear in the second query. |
| OUTER UNION | Concatenates (appends) the results from both queries. |

## Demystifying Join Algorithms

The SQL procedure contains an optimizer whose purpose is to use the best plan for query execution. A join algorithm locates, for each distinct value of the join attributes, an ordered list of elements in each relation that display that value. The SQL optimizer uses criteria to determine which join algorithm to use to optimize the query. The join construct, the structure of the data, the definition of indexes, the availability of real memory, and other factors can influence the join algorithm that is selected by the optimizer. The specific details of each of the join algorithms are described below.

### Nested Loop

A nested loop join algorithm might be selected by the SQL optimizer when processing small tables of data where one table is considerably smaller than the other table, the join condition does not contain an equality condition, first row matching is optimized, or using a sort-merge or hash join has been eliminated. This algorithm operates by looping through the smaller of the tables looking for a matching key in the larger table. A nested loop join algorithm is extremely sensitive to the contents of the right table because it processes the right table for each row of the left table. For this reason, this join algorithm tends to be more CPU intensive than other choices, particularly as the table sizes increase.

### Sort-Merge

A sort-merge join algorithm might be selected by the SQL optimizer when the tables are small to medium size. This algorithm operates by first sorting the tables of data (if necessary) using one or more key columns, and then, for each row in the left table, the algorithm reads all matching rows in the right table. The SQL optimizer considers using a sort-merge join algorithm when the conditions for using an index or hash join algorithm have been eliminated from consideration.

### Index

An index join algorithm might be selected by the SQL optimizer when indexes created on each of the columns participating in the join relationship will improve performance. This algorithm operates by looking up each row of the smaller table by accessing the index of the larger table. The SQL optimizer considers using an index join algorithm when the larger table has an associated index with all the join keys, the tables are related with an equality condition, and/or join conditions use the AND operator between multiple expressions.

### Hash

A hash join algorithm might be selected by the SQL optimizer when sufficient memory is available to the system, and the BUFFERSIZE option is large enough to store the smaller of the tables into memory. This algorithm operates by sequentially scanning the larger table and performing row-by-row lookup against the smaller table. The SQL optimizer considers using a hash join algorithm when an index join algorithm has been eliminated from consideration.

## Influencing Joins with a Little Magic

The SQL procedure supports various options to influence the execution of specific join algorithms. The following SQL procedure options are available:
