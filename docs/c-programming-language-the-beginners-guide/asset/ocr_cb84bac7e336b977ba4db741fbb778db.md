```
```
day;
day; day; day;
day; day;
day; day; day;
day;
day; day; day;

day; day;
day; day; day;
day; day; day;
day; day; day;
day; day; day; day; day; day; day;
day;
day;
day;
day;
day;
```
```

In this code, you see definitions for two structures. The first, is defined at line 6. It holds members year, month, and day. The second structure, is declared at line 11. It contains a name array, but also the date structure in the form of a *birthday* variable.

A person variable structure *friend* is declared at line 15. Lines 17 through 20 build a friend variable and *strcpy* is used to assign the string. For the structure member *birthday*, note how two dots are used to fill in the substructure members in lines 18, 19, and 20. That’s how it works. That is how structures within structures are referenced. Build and run this code.