```
CONSTRAINT TS_MANUFACTURER_ID FOREIGN KEY
(MANUFACTURER_ID)
REFERENCES PRODUCT_MANUFACTURERS (MANUFACTURER_ID) ); ¹⁹
```

You may consider the two lines at the bottom as the constraint's definition. The constraint's name, TS_MANUFACTURER_ID, comes after the keyword CONSTRAINT. You don't need to specify a name for your constraints since SQL will generate one for you in case this information is missing. On the other hand, you may want to set the name of your constraint manually since that value appears in errors (i.e. when SQL commands violate an existing constraint). In addition, the names you will provide are more recognizable than system-generated ones.

Next, you should set the kind of constraint you want to use. Then, enter the name of your referencing column (MANUFACTURER_ID for the current example). You will then place the constraint on that column. If you are dealing with multiple columns, you must separate the names using commas. Afterward, type REFERENCES as well as the referenced table's name. Finally, enter the name of your referenced column.

That's it. Once you have defined this constraint, the MANUFACTURER_ID column of PRODUCT_NAMES won't take values except those that are already listed in the PRODUCT_MANUFACTURERS table's primary key. As you can see, a foreign key doesn't need to hold unique values. You may repeat the values inside your foreign keys as many times as you want, unless you placed the UNIQUE constraint on the column you're working on.

Now, let's apply this constraint on multiple columns. You should master this technique before studying the remaining elements of the constraint's syntax. For this example, let's use two tables: BOOK_AUTHORS and BOOK_GENRES.

The table named BOOK_AUTHORS has a primary key defined in the AUTHOR_NAME and AUTHOR_DOB columns. The SQL statement found below generates a table called BOOK_GENRES. This table has a foreign key consisting of the AUTHOR_DOB and DATE_OF_BIRTH columns.

```
CREATE TABLE BOOK_GENRES
(AUTHOR_NAME CHARACTER (50) ,
DATE_OF_BIRTH DATE,
GENRE_ID INT,
CONSTRAINT TS_BOOK_AUTHORS FOREIGN KEY ( AUTHOR_NAME,
```