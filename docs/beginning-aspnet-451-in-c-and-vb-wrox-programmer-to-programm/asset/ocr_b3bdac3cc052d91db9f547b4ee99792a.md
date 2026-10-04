# CHAPTER 12

# Exercise 1 Solution

The DELETE statement fails because there is a relationship between the Id of the Genre table and the GenreId of the Review table. As long as this relationship is in effect, you cannot delete genres that have reviews attached to them. To be able to delete the requested genre, you need to delete the associated reviews first, or assign them to a different genre using an UPDATE statement. Exercise 4 shows you you can accomplish this.

# Exercise 2 Solution

The relationship between the Genre and Review tables is a one-way relationship. The relationship enforces the GenreId assigned to a review must exist as an Id in the Genre table. At the same time, it blocks you from deleting genres that have reviews attached to them. However, the relationship doesn't stop you from deleting rows from the Review table.

# Exercise 3 Solution

To delete reviews with an Id of 100 or less, you need the following SQL statement:

```
DELETE From Review Where Id <= 100
```

# Exercise 4 Solution

Before you delete the genre, you need to reassassign the existing reviews to a new genre first. You can do this with the following UPDATE statement:

```
UPDATE Review Set GenreId = 11 WHERE GenreId = 4
```

This assigns the GenreId of 11 to all reviews that previously have their GenreId set to 4. In this means that the genre with an Id of 4 no longer has reviews attached to it, so you can now remove it with the following SQL statement:

```
DELETE FROM Genre WHERE Id = 4
```

# Exercise 5 Solution

To update the name you need to execute an UPDATE statement. To limit the number of affected rows to just the Rock genre, you need to use a WHERE clause. You can use the WHERE clause to filter the rows based on the genre's Id or its Name. The following SQL statements are functionally equivalent:

```
UPDATE Genre Set Name = 'Punk Rock' Where Id = 7
UPDATE Genre Set Name = 'Punk Rock' WHERE Name = 'Rock'
```

This code assumes that the current Rock genre has an Id of 7.