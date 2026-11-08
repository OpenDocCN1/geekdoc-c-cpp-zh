
## 6.1 A Series of IF Statements—The Logical Lookup

The simplest form of a table lookup makes use of the IF-THEN statement. Although easy to code, this is one of the slowest table lookup methods. Essentially this technique creates the new variable with its associated value through the use of IF-THEN processing. Effectively we are ‘hard coding’ the clinic name within the program. This technique is demonstrated in the following DATA step.

```sas
data demogname;
  set advrpt.demog(keep=clinnum lname fname);
  length clinnum $35;
  if clinnum='011234' then clinname = 'Boston National Medical';
  if clinnum='014321' then clinname = 'Vermont Treatment Center';
  if clinnum='107211' then clinname = 'Portland General';
  if clinnum='108531' then clinname = 'Seattle Medical Complex';
  if clinnum='023910' then clinname = 'New York Metro Medical Ctr';
  if clinnum='024477' then clinname = 'New York General Hospital';
  run;
```

The problem with this approach is that it is not practical if there are more than a very few codes to lookup; besides this is VERY inefficient. SAS must execute each IF statement even if an earlier IF statement was found to be true. To make matters worse, IF statements require a fair bit of processing time.

This is an example of a 100% lookup. It is a sequential search and one where every code is checked regardless of whether or not the answer has already been found.

## 6.2 IF-THEN/ELSE Lookup Statements

A substantially faster method than the IF-THEN, is to use the IF-THEN / ELSE statement combination. The following DATA step executes more quickly than the previous one because as soon as one IF statement is found to be true, its associated ELSE is not executed. Consequently as soon as an expression is found to be true, none of the remaining IF-THEN / ELSE statements are executed. This technique can be made somewhat faster if the more likely outcomes are placed earlier in the list.

```sas
data demogname;
  set advrpt.demog(keep=clinnum lname fname);
  length clinnum $35;
  if clinnum='011234' then clinname = 'Boston National Medical';
  else if clinnum='014321' then clinname = 'Vermont Treatment Center';
  else if clinnum='107211' then clinname = 'Portland General';
  else if clinnum='108531' then clinname = 'Seattle Medical Complex';
  else if clinnum='023910' then clinname = 'New York Metro Medical Ctr';
  else if clinnum='024477' then clinname = 'New York General Hospital';
  run;
```

In terms of performance efficiency this technique is similar to that of the DATA step’s SELECT statement and the CASE statement in SQL. The SELECT statement is on par with the IF-THEN / ELSE combination when performing table lookups. It can even be a bit faster (Virgle, 1998). Again processing time is minimized when the most likely match is located early in the list.

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

Interestingly Virgle (1998) found that the efficiency of the SELECT statement can sometimes be enhanced by placing the entire expression on the WHEN statement.

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

There are two overriding issues with these techniques. The primary problem is that the search is sequential. When the list is long the average number of comparisons goes up quickly, even when you carefully order the list. The second, but no less important, issue is that these techniques hard code the values in the program. This is just not smart programming.

Fortunately, the other lookup techniques in this chapter not only avoid hard coding altogether, but also minimize the need for sequential searches.

## 6.3 DATA Step Merges and SQL Joins

The use of joins in an SQL step and the MERGE in the DATA step is another very common way to perform table lookups by matching values between two data sets. The MERGE statement (when used with the BY statement as it usually is) requires sorted or indexed data sets, while the SQL step does not. There are advantages and disadvantages to both processes.

### MERGE Statement

The MERGE statement is used to combine two or more data sets. For the purpose of this discussion, one of these data sets will contain the information that is to be looked up. The BY statement is used to make sure that the observations are correctly aligned. The BY statement

### SQL Join

When using SQL, the merging process is called a *join*. The SQL join operations do not require sorting and can be more efficient than the DATA step MERGE, unless the tables are so large that they do not fit well into memory.

Just because an SQL join does not require the incoming data to be sorted, does not mean that no resources are going to be expended in preparation for the join (lookup). Hidden from view, but within the processing of the SQL step, lookup techniques are being applied. These behind the scenes operations are very similar to the hash techniques that we can explicitly apply and control in the DATA step (see Sections 6.7 and 6.8).

There are a number of different types of joins within SQL, and one that closely matches the previous step is shown below.

In this example we have added the requirement (through the use of a WHERE clause ❷) that the clinic number be in both data tables. The WHERE clause is used to select rows that have matching values of CLINNUM on both incoming tables. This is a more stringent criteria than was used in the DATA step shown above ❶.

```sas
proc sql noprint;
   create table demognames2 as
      select a.clinnum, b.clinname, lname, fname
      from advrpt.demog a, advrpt.clinname b
      where a.clinnum=b.clinnum; ❷
   quit;
```

SQL does not require either of the two data sets to be sorted prior to the join, and unless we specifically request that the resulting data table be sorted (ORDER BY clause) it will reflect the order of the incoming data. This can be seen in the order of the clinic number in the PROC PRINT results shown below.

6.3 Lookup By Joining or Merging Two Tables  
10 Observations of the Joined Data

| Obs | clinnum | clinname | lname | fname |
|---:|---:|---|---|---|
| 1 | 049060 | Atlanta General Hospital | Adams | Mary |
| 2 | 082287 | Denver Security Hospital | Adamson | Joan |
| 3 | 066789 | Austin Medical Hospital | Alexander | Mark |
| 4 | 063742 | Houston General | Antler | Peter |
| 5 | 023910 | New York Metro Medical Ctr | Atwood | Teddy |
| 6 | 066789 | Austin Medical Hospital | Banner | John |
| 7 | 046789 | Tampa Treatment Complex | Baron | Roger |
| 8 | 049060 | Atlanta General Hospital | Batell | Mary |
| 9 | 095277 | San Francisco Bay General | Block | Will |
| 10 | 031234 | Bethesda Pioneer Hospital | Candle | Sid |

*....portions of the table are not shown....*

## 6.4 Merge Using Double SET Statements

There are a number of schemes that have been published that utilize two SET statements in the same DATA step. These SET statements replace the single MERGE statement and the programmer takes charge of the joining process (keeping the two data sets in sync). These techniques can be faster but more complicated than a MERGE. However they do still require that both incoming data sets be sorted.
