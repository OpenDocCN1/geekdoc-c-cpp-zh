# Multiple Delimiters

It is possible to read delimited input streams that contain more than one delimiter. In the following small example two delimiters, a comma and a slash are both used to delimit the data values.

```
```
data imports;
infile cards dlm=',/';
input id importcode $ value;
cards;
14,1,13
25/Q9,15
6,D/20
run;
```
```

| Obs | id | importcode | value |
| --- | --- | --- | --- |
| 1 | 14 | 1 | 13 |
| 2 | 25 | Q9 | 15 |
| 3 | 6 | D | 20 |

Notice that the DLM option causes either the comma or the slash to be used as field delimiters, but not the slash comma together as a single delimiter (see the DLMSTR option below to create a single multiple character delimiter).

```
```
data imports;
retain dlmvar '/,'; ❶
infile cards dlm=dlmvar;
input id importcode $ value;
cards;
14,1,13
25/Q9,15
6,D/20
run;
```
```

+   - ❶ Because the INFILE statement is executed for each observation, the value assigned to the DLM option does not necessarily need to be a constant. It can also be a variable or can be changed using IF-THEN/ELSE logic. In the simplest form this variable could be assigned in a retain statement.
+   - ❷ This simple example demonstrates a delimiter that varies by observation. Here the first character of each line is the delimiter that is to be used in that line. The delimiter is read, stored, and then used on the INFILE statement. Here we are taking advantage of the executable nature of the INFILE statement.

```
```
data imports;
infile cards;
input dlmvar $1. ❷;
infile cards dlm=dlmvar; ❸
input @2 id importcode $ value;
cards;
,14,1,13
/25/Q9/15
~6~D~20
run;
```
```

# Using DLMSTR

Unlike the DLM option, which designates one or more delimiters, the DLMSTR option declares a specific list of characters to use as a delimiter. Here the delimiter is the sequence of characters comma-comma-slash (,,/). Notice in the LISTING of the IMPORT data set, that extra commas and slashes are read as data.

```
```
data imports;
infile cards dlmstr=',,/' ;
input id importcode $ value;
cards;
14,,/1/,,/13
25,,/Q9,,,/15
6,,/,D,,/20
run;
```
```

1.3.3g Use a delimiter string

| Obs | id | importcode | value |
| --- | --- | --- | --- |
| 1 | 14 | 1/ | 13 |
| 2 | 25 | Q9, | 15 |
| 3 | 6 | ,D | 20 |