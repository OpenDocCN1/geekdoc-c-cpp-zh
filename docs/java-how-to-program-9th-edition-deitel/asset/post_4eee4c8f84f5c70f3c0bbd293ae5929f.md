
## Software Engineering Observation 28.3

In general, you process results by knowing in advance the order of the columns in the result—for example, selecting AuthorID and LastName from table Authors ensures that the columns will appear in the result with AuthorID as the first column and LastName as the second column. Programs typically process result columns by specifying the column number in the result (starting from number 1 for the first column). Selecting columns by name avoids returning unneeded columns and protects against changes in the actual order of the columns in the table(s) by returning the columns in the exact order specified.

## Common Programming Error 28.4

If you assume that the columns are always returned in the same order from a query that uses the asterisk (*), the program may process the results incorrectly. If the column order in the table(s) changes or if additional columns are added at a later time, the order of the columns in the result will change accordingly.

## 28.4.2 WHERE Clause

In most cases, it’s necessary to locate rows in a database that satisfy certain selection criteria. Only rows that satisfy the selection criteria (formally called predicates) are selected. SQL uses the optional WHERE clause in a query to specify the selection criteria for the query. The basic form of a query with selection criteria is

```
SELECT columnName1, columnName2, ... FROM tableName WHERE criteria
```

For example, to select the Title, EditionNumber and Copyright columns from table Titles for which the Copyright date is greater than 2010, use the query

```
SELECT Title, EditionNumber, Copyright
FROM Titles
WHERE Copyright > '2010'
```

Strings in SQL are delimited by single (') rather than double (") quotes. Figure 28.12 shows the result of the preceding query.

| Title | EditionNumber | Copyright |
|---|---|---|
| Visual Basic 2010 How to Program | 5 | 2011 |
| Visual C# 2010 How to Program | 4 | 2011 |
| Java How to Program | 9 | 2012 |
| C++ How to Program | 8 | 2012 |
| Android for Programmers: An App-Driven Approach | 1 | 2012 |

Fig. 28.12 | Sampling of titles with copyrights after 2010 from table Titles.

### Pattern Matching: Zero or More Characters

The WHERE clause criteria can contain the operators <, >, <=, >=, =, <> and LIKE. Operator LIKE is used for pattern matching with wildcard characters percent (%) and underscore (_). Pattern matching allows SQL to search for strings that match a given pattern.

A pattern that contains a percent character (%) searches for strings that have zero or more characters at the percent character’s position in the pattern. For example, the next query locates the rows of all the authors whose last name starts with the letter D:

```
SELECT AuthorID, FirstName, LastName
FROM Authors
WHERE LastName LIKE 'D%'
```

This query selects the three rows shown in Fig. 28.13—three of the five authors have a last name starting with the letter D (followed by zero or more characters). The % symbol in the WHERE clause’s LIKE pattern indicates that any number of characters can appear after the letter D in the LastName. The pattern string is surrounded by single-quote characters.

| AuthorID | FirstName | LastName |
|---|---|---|
| 1 | Paul | Deitel |
| 2 | Harvey | Deitel |
| 3 | Abbey | Deitel |

Fig. 28.13 | Authors whose last name starts with D from the Authors table.

## Portability Tip 28.1

See the documentation for your database system to determine whether SQL is case sensitive on your system and to determine the syntax for SQL keywords.

## Portability Tip 28.2

Read your database system’s documentation carefully to determine whether it supports the LIKE operator as discussed here.

### Pattern Matching: Any Character

An underscore (_) in the pattern string indicates a single wildcard character at that position in the pattern. For example, the following query locates the rows of all the authors whose last names start with any character (specified by _), followed by the letter o, followed by any number of additional characters (specified by %):

```
SELECT AuthorID, FirstName, LastName
FROM Authors
WHERE LastName LIKE '_o%'
```

The preceding query produces the row shown in Fig. 28.14, because only one author in our database has a last name that contains the letter o as its second letter.

| AuthorID | FirstName | LastName |
|---|---|---|
| 4 | Michael | Morgano |

Fig. 28.14 | The only author from the Authors table whose last name contains o as the second letter.

## 28.4.3 ORDER BY Clause

The rows in the result of a query can be sorted into ascending or descending order by using the optional ORDER BY clause. The basic form of a query with an ORDER BY clause is

```
SELECT columnName1, columnName2, ... FROM tableName ORDER BY column ASC
SELECT columnName1, columnName2, ... FROM tableName ORDER BY column DESC
```

where ASC specifies ascending order (lowest to highest), DESC specifies descending order (highest to lowest) and column specifies the column on which the sort is based. For example, to obtain the list of authors in ascending order by last name (Fig. 28.15), use the query

```
SELECT AuthorID, FirstName, LastName
FROM Authors
ORDER BY LastName ASC
```

| AuthorID | FirstName | LastName |
|---|---|---|
| 1 | Paul | Deitel |
| 2 | Harvey | Deitel |
| 3 | Abbey | Deitel |
| 5 | Eric | Kern |
| 4 | Michael | Morgano |

Fig. 28.15 | Sample data from table Authors in ascending order by LastName.

### Sorting in Descending Order

The default sorting order is ascending, so ASC is optional. To obtain the same list of authors in descending order by last name (Fig. 28.16), use the query

```
SELECT AuthorID, FirstName, LastName
FROM Authors
ORDER BY LastName DESC
```

| AuthorID | FirstName | LastName |
|---|---|---|
| 4 | Michael | Morgano |
| 5 | Eric | Kern |
| 1 | Paul | Deitel |
| 2 | Harvey | Deitel |
| 3 | Abbey | Deitel |

Fig. 28.16 | Sample data from table Authors in descending order by LastName.

### Sorting By Multiple Columns

Multiple columns can be used for sorting with an ORDER BY clause of the form

```
ORDER BY column1 sortingOrder, column2 sortingOrder, ...
```

where sortingOrder is either ASC or DESC. The sortingOrder does not have to be identical for each column. The query

```
SELECT AuthorID, FirstName, LastName
FROM Authors
ORDER BY LastName, FirstName
```

sorts all the rows in ascending order by last name, then by first name. If any rows have the same last-name value, they’re returned sorted by first name (Fig. 28.17).

| AuthorID | FirstName | LastName |
|---|---|---|
| 3 | Abbey | Deitel |
| 2 | Harvey | Deitel |
| 1 | Paul | Deitel |
| 5 | Eric | Kern |
| 4 | Michael | Morgano |

Fig. 28.17 | Sample data from Authors in ascending order by LastName and FirstName.

### Combining the WHERE and ORDER BY Clauses

The WHERE and ORDER BY clauses can be combined in one query, as in

```
SELECT ISBN, Title, EditionNumber, Copyright
FROM Titles
WHERE Title LIKE '%How to Program'
ORDER BY Title ASC
```

which returns the ISBN, Title, EditionNumber and Copyright of each book in the Titles table that has a Title ending with "How to Program" and sorts them in ascending order by Title. The query results are shown in Fig. 28.18.

| ISBN | Title | EditionNumber | Copyright |
|---|---|---|---|
| 0132404168 | C How to Program | 6 | 2010 |
| 0132662361 | C++ How to Program | 8 | 2012 |
| 0132575663 | Java How to Program | 9 | 2012 |
| 0132152134 | Visual Basic 2010 How to Program | 5 | 2011 |
| 0132151421 | Visual C# 2010 How to Program | 4 | 2011 |

Fig. 28.18 | Sampling of books from table Titles whose titles end with How to Program in ascending order by Title.

## 28.4.4 Merging Data from Multiple Tables: INNER JOIN

Database designers often split related data into separate tables to ensure that a database does not store data redundantly. For example, in the books database, we use an AuthorISBN table to store the relationship data between authors and their corresponding titles. If we did
