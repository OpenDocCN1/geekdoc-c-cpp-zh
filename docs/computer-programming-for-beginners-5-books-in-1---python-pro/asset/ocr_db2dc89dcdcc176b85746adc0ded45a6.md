```
```sql
(AUTHOR_ID INT,
AUTHOR_NAME CHARACTER (50) PRIMARY KEY ,
PUBLISHER_ID INT ) ;
```
```

If you want to apply PRIMARY KEY on multiple columns (or store it as another definition), you may use it on the tabular level:

```
```sql
CREATE TABLE FICTION_NOVEL_AUTHORS
(AUTHOR_ID INT,
AUTHOR_NAME CHARACTER (50) ,
PUBLISHER_ID INT,
CONSTRAINT PK_AUTHOR_ID PRIMARY KEY (AUTHOR_ID,
AUTHOR_NAME ) ) ;
```
```

This approach places a primary key on two columns (i.e. AUTHOR_ID and AUTHOR_NAME). That means the paired values of the two columns need to be unique. However, duplicate values may exist inside any of the columns. Experienced database users refer to this kind of primary key as a “superkey.” The term “superkey” means that the primary key exceeds the number of required columns.

In most cases, you need to set both UNIQUE and PRIMARY KEY constraints on a table. To achieve this, you just have to define the involved constraints, as usual. For instance, the code given below applies both of these constraints:

```
```sql
CREATE TABLE FICTION_NOVEL_AUTHORS
(AUTHOR_ID INT,
AUTHOR_NAME CHARACTER (50) PRIMARY KEY ,
PUBLISHER_ID INT,
CONSTRAINT UN_AUTHOR_NAME UNIQUE (AUTHOR_NAME) ) ;
```
```

The following code will give you the same result:

```
```sql
CREATE TABLE FICTION_NOVEL_AUTHORS
(AUTHOR_ID INT,
AUTHOR_NAME CHARACTER (50) -> UNIQUE,
PUBLISHER_ID INT,
```
```