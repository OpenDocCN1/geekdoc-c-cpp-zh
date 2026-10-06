# 54 CHAPTER 3 WRITING BASIC QUERIES

```
foreach (string s in q)
Console.WriteLine(s);
```

# Output 3-4

+   - Koala
- Spider
- Snake
- Shark
- Jellyfish

# How to Change the Return Type (Select Projection)

When you write queries against a database system in SQL, specifying a set of columns to return is second nature. The goal is to limit the columns returned to only those necessary for the query in order to improve performance and limit network traffic (the less data transferred, the better). This is achieved by listing the column names after the Select clause in the following format. In most cases, only the columns of interest are returned using the SQL syntax form:

```
Select * from Contacts
```

```
Select ContactId, FirstName, LastName from Contacts
```

The first query will return every column (and row) of the contacts table; the second will return only the three columns explicitly listed (for every row), saving server and network resources. The point is that the SQL syntax allows a different set of rows that does not match any existing database table, view, or schema to be the structure used in returning data. Select projections in LINQ expressions allow us to achieve the same task. If only few property values are needed in the result set, those properties or fields are the only ones returned. LINQ selection projections allow varied and powerful control over how and what data shape is returned from a query expression.