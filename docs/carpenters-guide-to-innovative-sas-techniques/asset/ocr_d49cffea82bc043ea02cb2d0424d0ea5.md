The SELECT statement is on par with the IF-THEN / ELSE combination when performing table lookups. It can even be a bit faster (Virgle, 1998). Again processing time is minimized when the most likely match is located early in the list.

```
```sas
data demogname;
    set advrpt.demog(keep=clinnum lname fname);
    select(clinnum);
       when ('011234') clinname='Boston National Medical';
       when ('014321') clinname='Vermont Treatment Center';
       when ('107211') clinname='Portland General';
       when ('108531') clinname='Seattle Medical Complex';
       when ('023910') clinname='New York Metro Medical Ctr';
       when ('024477') clinname='New York General Hospital';
       otherwise;
    end;
    run;
```
```

Interestingly Virgle (1998) found that the efficiency of the SELECT statement can sometimes be enhanced by placing the entire expression on the WHEN statement.

```
```sas
data demogname;
    set advrpt.demog(keep=clinnum lname fname);
    select;
       when(clinnum='011234') clinname='Boston National Medical';
       when(clinnum='014321') clinname='Vermont Treatment Center';
       when(clinnum='107211') clinname='Portland General';
       when(clinnum='108531') clinname='Seattle Medical Complex';
       when(clinnum='023910') clinname='New York Metro Medical Ctr';
       when(clinnum='024477') clinname='New York General Hospital';
       otherwise;
    end;
    run;
```
```

There are two overriding issues with these techniques. The primary problem is that the search is sequential. When the list is long the average number of comparisons goes up quickly, even when you carefully order the list. The second, but no less important, issue is that these techniques hard code the values in the program. This is just not smart programming.

Fortunately, the other lookup techniques in this chapter not only avoid hard coding altogether, but also minimize the need for sequential searches.

# 6.3 DATA Step Merges and SQL Joins

The use of joins in an SQL step and the MERGE in the DATA step is another very common way to perform table lookups by matching values between two data sets. The MERGE statement (when used with the BY statement as it usually is) requires sorted or indexed data sets, while the SQL step does not. There are advantages and disadvantages to both processes.

# MERGE Statement

The MERGE statement is used to combine two or more data sets. For the purpose of this discussion, one of these data sets will contain the information that is to be looked up. The BY statement is used to make sure that the observations are correctly aligned. The BY statement